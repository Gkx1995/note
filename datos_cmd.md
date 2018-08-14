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
/usr/datos/datos_cli addstore --sname demo --stype vfs_store --surl file://localhost/vfsgaurav

# add source
/usr/datos/datos_cli addsource --source_ip 10.30.101.49 --source_port 27110 --app_instance_id queryable_source --source_user_name centos --source-type mongo --source-auth-keyfile ~/.ssh/id_rsa

# generate rand entry
python ~/bigdatos/tools/mongo-populate/mongo_strings_bulk.py --host 10.2.3.194 --port 27017 --db_name xy_db --num_entries 10000 --doc_size 10240 --coll_name colla
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

