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
# before add source, need to setup mongo
~/workspace/bigdatos/scripts/regression_test/setup/mongo_setup_default -r 2 -m 3

# add store
/usr/datos/datos_cli addstore --sname queryable_store --stype vfs_store --surl ~/store/

# add source
/usr/datos/datos_cli addsource --source_ip 10.30.101.49 --source_port 27110 --app_instance_id queryable_source --source_user_name centos --source-type mongo --source-auth-keyfile ~/.ssh/id_rsa

# add schedule
/usr/datos/datos_cli addschedule --schedule-name quick_queryable --interval 2m --retention-period 10m --retention-frequency 10m

# add policy
/usr/datos/datos_cli addpolicy  --policy-name queryable_policy_datos_guys --mgmt-object xy_db.coll_datos_guys --src-type mongo --cluster-name queryable_source --stg-name queryable_store --schedule-name quick_queryable --start-time 0s



# retrieve 
/usr/datos/datos_cli retrieve --spid fbb9c726-a009-11e8-9ab1-0016a64ebb16 --source-name queryable_source --mgmt-object xy_db.colla --target-name queryable_source --target-mgmt-obj xy_db.kai --version-time 1534283130 --dest-path ~/retrieve_dir/

/usr/datos/datos_cli retrieve --spid a042024a-a01e-11e8-a6ac-0016a64ebb16 --source-name queryable_source --mgmt-object xy_db.coll_datos_guys --target-name queryable_source --target-mgmt-obj xy_db.coll_datos_with_query --version-time 1534291516 --dest-path ~/retrieve_dir/ --target-query "where utf8 name = Kai and int32 age < 50"

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
docker run -it -v /home/centos/codebase/bigdatos_queryable/bigdatos:/kai buildvm:kai
```

```js
for (var i = 1; i <= 100; i++) {db.colla.insert({x: i, "str": i})}
```

