```bash
# reg test
./datos_regression_driver -s Sample_Regression_Setup_wiredTiger -w mongo -f Testsuite.kai
```

```bash
# start datos UI
datos/ui/node_modules/bower/bin/bower install bower.json
cd datos/ui
npm install package.json
Scripts/datos_setup.sh
./datos_cluster stop && rm -rf logs && ./datos_cluster start --reset
```

```bash
~/workspace/bigdatos/scripts/datos_setup.sh
rm -rf ~/store
mkdir ~/store
# before add source, need to setup mongo
~/workspace/bigdatos/scripts/regression_test/setup/mongo_setup_default -r 2 -m 3

# generate rand entry
python ~/workspace/bigdatos/tools/mongo-populate/mongo_queryable_dummy_docs.py --host 10.30.101.49 --port 27017 --db_name xy_db --num_entries 1000 --coll_name coll_datos_guys

# add store
/usr/datos/datos_cli addstore --sname queryable_store --stype vfs_store --surl /home/centos/store/

# add source 
/usr/datos/datos_cli addsource --source_ip 10.30.101.49 --source_port 27110 --app_instance_id queryable_source --source_user_name centos --source-type mongo --source-auth-keyfile ~/.ssh/id_rsa

# add schedule
/usr/datos/datos_cli addschedule --schedule-name quick_queryable --interval 2m --retention-period 10m --retention-frequency 10m

# add policy
/usr/datos/datos_cli addpolicy  --policy-name queryable_policy_collb --mgmt-object xy_db.collb --src-type mongo --cluster-name queryable_source --stg-name queryable_store --schedule-name quick_queryable --start-time 0s


# retrieve 
/usr/datos/datos_cli retrieve --spid c489bed4-a26e-11e8-854d-0016a64ebb16 --source-name queryable_source --mgmt-object xy_db.colla --target-name queryable_source --target-mgmt-obj xy_db.kai --version-time 1534551145 --dest-path ~/retrieve_dir/

# retrieve for datos guys 1
/usr/datos/datos_cli retrieve --spid e38717de-ac94-11e8-9f27-0016a64ebb16 --source-name queryable_source --mgmt-object xy_db.coll_datos_guys --target-name queryable_source --target-mgmt-obj xy_db.coll_datos_with_query_2 --version-time 1535661723 --dest-path ~/retrieve_dir/ --target-query "select name,age,info.pet.species,info.lucky_number WHERE int32 info.lucky_number.0.a > 30 AND ((utf8 info.pet.species = cat OR utf8 info.pet.species = dog) AND utf8 info.birth_place = US)"

# retrieve for datos guys 2
/usr/datos/datos_cli retrieve --spid 261c6e0c-a0d6-11e8-9cbf-0016a64ebb16 --source-name queryable_source --mgmt-object xy_db.coll_datos_guys --target-name queryable_source --target-mgmt-obj xy_db.coll_datos_with_query_2 --version-time 1534372978 --dest-path ~/retrieve_dir/ --target-query "where utf8 name = Kai and int32 age < 50 and bool married = 1 and utf8 minkey key_1 * and maxkey key_2 *"

# retrieve for datos guys 3
/usr/datos/datos_cli retrieve --spid 261c6e0c-a0d6-11e8-9cbf-0016a64ebb16 --source-name queryable_source --mgmt-object xy_db.coll_datos_guys --target-name queryable_source --target-mgmt-obj xy_db.coll_datos_with_query_2 --version-time 1534372978 --dest-path ~/retrieve_dir/ --target-query "where utf8 name = 'Gaurav Old' or utf8 name = 'Gaurav New' and int32 age < 50 and bool married = 1"

# generate rand entry
python ~/workspace/bigdatos/tools/mongo-populate/mongo_queryable_dummy_docs.py --host 10.30.101.49 --port 27017 --db_name xy_db --num_entries 1000 --coll_name coll_datos_guys

# get version
/usr/datos/datos_cli getversions --source-name queryable_source

/usr/datos/datos_cli getversions --source-name queryable_source --print-pretty no
```

```bash
#gaurav vm
ssh -i key4datos.pem centos@10.7.1.122

# copy restore_rate_limiter
scp -i ~/key4datos.pem centos@10.7.1.122:/home/centos/codebase/bigdatos_queryable/bigdatos/datos/init_code/restore_rate_limiter datos/init_code/

# cd to step5 and build docker
docker build  `pwd` -t buildvm:kai

#run docker
docker run -it -v /home/centos/workspace/bigdatos:/kai docker.io/rdiodev/datos:buildvm.latest
```

```js
for (var i = 1; i <= 100; i++) {db.colla.insert({x: i})}
```







#### Setup RecoverX for multiple node

0. ##### re-installation

   ###### Build with params

   http://10.2.3.175:8080/job/Build_Request_CentOS_6.8/build?delay=0sec

   BRANCH: trunk

   EMAIL: you email

   Build and wait. Tapically it takes ~30 min. After that you will receive a email from reg_tester@datos.io.

   ###### Close firewall

   Open ports that we are using. Normally we should check these ports and open them, but since we are setting up Rx for internal use, we just disable firewalls on all nodes including Rx node and data source nodes.

   ```shell
   sudo service iptables stop
   sudo chkconfig iptables off
   ```

   ###### Configure Maximum SSH Sessions

   In `/etc/ssh/sshd_config` on all nodes, set `MaxSessions` to 500 and `MaxStartups` to "500:1:500"

   ###### Config Rx Nodes

   On Rx node.

   `/etc/security/limits.conf`, set these params.

   ```shell
   *    hard    nproc    unlimited
   *    soft    nproc    unlimited
   *    hard    nofile   64000
   *    soft    nofile   64000
   ```

   Edit the `nproc` parameter. For RHEL 6 / centOS 6 the parameter is in `/etc/security/limits.d/90-nproc.conf`. For RHEL 7 / centOS 7, the parameter is in `/etc/security/limits.d/20-nproc.conf.`

   ```shell
   *    hard    nproc    unlimited
   *    soft    nproc    unlimited
   ```

   Verify the changes above by running the following command:

   ```shell
   $ ulimit -a
   ```

   

1. ##### Download build tarball from S3, run this py script with s3 url as input argument.<s3://datos_builds/datos_3.0.0_CentOS_6.7_2018-08-21-17-09_cdb8a42.tar.gz>

   S3 will keep this build for 30 days. If you want to reinstall Rx after 30 days, repeat step 0.

   ```python
   import argparse
   import boto
   parser = argparse.ArgumentParser()
   parser.add_argument('url', help='S3 URL for the build')
   args = parser.parse_args()
   bucket_name, build_file_name = args.url.split('/')[-2:]
   conn = boto.connect_s3("AKIAIFHNXLAM7XLJZ32Q","WxOdPsjqSUnCzrd3qRPnoieS35ZM5ka0uex4oCJQ")
   bucket = conn.get_bucket(bucket_name)
   key = bucket.get_key(build_file_name)
   key.get_contents_to_filename(build_file_name)
   ```

2.  ##### Unzip tarball

   ```shell
   tar -xvzf datos_3.0.0_CentOS_6.7_2018-08-21-17-09_cdb8a42.tar.gz
   ```

3. ##### Install. change IP to your machine.

   ```shell
   ./install_datos -i <Rx_node_ip> -t /path/to/dir --skip-eula-check
   ```

4. ##### Install MongoDB 3.4 on source node

   https://docs.mongodb.com/v3.4/tutorial/install-mongodb-on-linux/

5. ##### Setup mongo cluster on a single node

   Change IP in `mongo_setup_default`

   ```shell
   MONGOCONFIGVMIP=<Your_source_node_ip>
   ```

   Set up 2 replica sets for Mongo cluster, and each replica set has 3 members.

   ```shell
   ./mongo_setup_default -r 2 -m 3
   ```













