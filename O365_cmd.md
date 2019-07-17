##### 1. build & deploy service

`sp-service-build korg-job-index-o365-mailbox`

`sp-service-deploy -d dev-131 korg-job-index-o365-mailbox`

##### 2. find customer db

`sp-port-forward -d dev-131 exocompute cloudsql o365-cloud-manager`

`sp-sql localhost`

`use spark;`

`select * from Accounts;`

`use <db_for_your_acct>`

##### 3. redeploy exocompute resource group

1. in your customer db, `delete from o365_mailboxes; delete from o365_calendars; delete from snapshots; delete from snappables; delete from o365_users; delete from o365_organizations; delete from o365_azure_exocompute_clusters; delete from managed_object;`
2. Add new O365 subscription setup `o365rubrik.onmicrosoft.com` rdnn14`neboysa.omcikus@rdnn14.onmicrosoft.com` `Serbia%^56`
3. Rdnn16 `scott.wang@rdnn16.onmicrosoft.com / Scaledata!@34`

##### 4. events show up in seperate sections in UI, did not set eventSeriesID, which is taskChainUUID

##### 5. When lint complains, run `gol` or `goimport local rubrik -w .`

##### 6. Find Error log by Error code, which is taskchainUUID

`use spark;`

`show tables;`

`select * from taskchains where taskchainUUID = <error code>`

`find your number and search at gcp console`

##### 7. Cache issue when `./spark env setup` task failed, ask @satyam

##### 8. when you want to update with `master` branch, first `git fetch && git pull` to update your local `master` branch, then do `sp-rebase` on your local feature branch, and it would update your feathure branch with your change applied.

#####9. push image to azure (Update exocompute)

first: `sp-service-build <service> && sp_service-deploy -d dev-131 <service>`

then:`

*find exocompute_Id* : `select id from o365_azure_exocompute_clusters;`

`6573ddc8-d746-496a-84e1-1d32ef582018` if you did not change it

*Account_id*: Polatis UI `kai`

##### 10. Run `sp-bazel-go` whenever you update diff

#####11. about `backport` in `git`

#####12.  search for persistent data

`select progress from taskchains;`

#####find yout data

`describe korg_job_backup_o365_mailbox;`

`select * from korg_job_backup_o365_mailbox where mailbox_id = "18c86a2d-cd85-4323-aff3-c578d9cecf74"`

`selct * from taskchains where taskchain_uuid = "e556f0dd-4d30-4d55-86f2-5ca5bfd515ed"`

#####13. Develop and test api server

https://rubrik.atlassian.net/wiki/spaces/SPARK/pages/461931179/API-Server+Development+Debugging

if some error occurs, just `sp-service-build` to make and build all service and then do `make dev-local` inside api-server folder

need to ask for userId in api-server UI, so right click on polaris UI `events` panel and click `inspect` and use `Apollo` to request all the 

```bash
query{
  getAllUsersOnAccount{
    id
    email
  }
}
```



##### 15. missing dependencies, run `sp-bazel-go`, basically whenever you import new dependencies you run this cmd



##### 16. go to exocompute log

go to `portal.azure.com` --> `resource groups` --> `view Kubernetes dashboard` --> copy and paste the third cmd to terminal and run



#####17. get `app_id` and credentials: `select * from rubrik_azure_enterprize_app;`



##### 18. delete all resumable files

`az storage blob delete-batch --source rubrik-o365-backups --account-key lRPLESEt/XTxjgRrgXRYn/UbJ1nnEYuBZVfdrzCNp+3sfQB9Ms5YtvbvcEt4tPUfJ2hxgxAx+o/8Bmp+foY5Mw== --account-name dev131san5 --pattern "????????-????-????-????-????????????/????????-????-????-????-????????????/????????-????-????-????-????????????.mfe"`

````az storage blob delete-batch --source rubrik-o365-backups --account-key lRPLESEt/XTxjgRrgXRYn/UbJ1nnEYuBZVfdrzCNp+3sfQB9Ms5YtvbvcEt4tPUfJ2hxgxAx+o/8Bmp+foY5Mw== --account-name dev131san5 --pattern *resumeartifacts*````





##### 19. lookinf for customer issues

1. Port forward to prod`sp-prod-cloudsql-proxy -d prod-002 start`
2. in a separate windows, password to database
3. `use spark`
4. `select * from taskchains where id ={id} and account_id = {customer_name} and job_type = "korg-job-backup-o365-mailbox"`



#### 20. troubleshooting aks dashboard

`az aks get-credentials -g kaiRDNN14RG -n Rubrik-C3-qcMqNd0WkVo2kPeGIEXz`

`kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard`





##### 21. grpc endpoint launch pod

`sp-grpc --service exocompute -- localhost:50091 exocompute.Exocompute.PodLaunch -d '{"account_id": "kai", "cluster_id": "cb3a979f-4dd3-4216-91d9-3a2534d8f659", "containers": {"container_name": "o365-mock-service", "image_name": "o365-mock-service", "launch_args": "hhh"}}';`

`sp-grpc --service exocompute -- localhost:50091 exocompute.Exocompute.ImagePush -d '{ "account_id": "kai", "cluster_id": "c80ead8d-9b69-4ba9-a6cd-ffc2913f466b", "image_name": "o365-mock-service", "image_tag": "latest"}'`



#### 22. On-demand refresh

`sp-korg-run-on-demand-job -d dev-131 --job-type refresh-o365-org --job-info '{"OrgUUID": "e44db7ab-9d06-4824-bf4d-5f885f8c9bd4","AccountID": "kai"}'`

`sp-korg-run-on-demand-job -d dev-131 --job-type backup-o365-mailbox --job-info '{"MailboxUUID": "853e5740-dcbe-4ce3-989a-59bcd3c1b26f","AccountID": "kai"}'`



##### 23. delete all subscriptions

in customerdb 

`delete from o365_mailboxes; delete from o365_calendars; delete from snapshots; delete from snappables; delete from o365_users; delete from o365_organizations; delete from o365_azure_exocompute_clusters; delete from managed_object;`

in spark

`delete from korg_job_backup_o365_mailbox; delete from korg_job_index_o365_mailbox;`


