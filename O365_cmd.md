#####1. build & deploy service

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

##### 4. events show up in seperate sections in UI, did not set eventSeriesID, which is taskChainUUID

##### 5. When lint complains, run `gol` or `goimport local rubrik -w .`

##### 6. Find Error log by Error code, which is taskchainUUID

`use spark;`

`show tables;`

`select * from taskchains where taskchainUUID = <error code>`

`find your number and search at gcp console`

##### 7. Cache issue when `./spark env setup` task failed, ask @satyam

##### 8. when you want to update with `master` branch, first `git fetch && git pull` to update your local `master` branch, then do `sp-rebase` on your local feature branch, and it would update your feathure branch with your change applied.

#####9. push image to azure

`sp-grpc --service exocompute -- localhost:50091 exocompute.Exocompute.ImagePush -d '{"account_id": "kai", "cluster_id": "6573ddc8-d746-496a-84e1-1d32ef582018", "image_name": "o365-exo-snapshot", "image_tag": "latest"}'`

*find exocompute_Id* : `select * from o365_azure_exocompute_clusters`

`6573ddc8-d746-496a-84e1-1d32ef582018` if you did not change it

*Account_id*: Polatis UI `kai`