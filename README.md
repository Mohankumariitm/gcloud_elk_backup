mkdir ~/elasticsearch-backup/

sudo nano /opt/bitnami/elasticsearch/config/elasticsearch.yml
path.repo: ["/home/mohan_nehil_gmail_com/elasticsearch-backup"]


sudo chown -R elasticsearch:elasticsearch /home/mohan_nehil_gmail_com/elasticsearch-backup/

sudo /opt/bitnami/ctlscript.sh restart elasticsearch

curl -XPUT "http://127.0.0.1:9200/_snapshot/final_backup" -H 'Content-Type: application/json' -d'
{
   "type": "fs",
   "settings": {
       "compress" : true,
       "location": "/home/mohan_nehil_gmail_com/elasticsearch-backup"
   }
}'


curl -XPUT "http://127.0.0.1:9200/_snapshot/final_backup/snapshot_1?wait_for_completion=true"


tar -zcvf elasticsearch-backup-gcloud-2.tar.gz  ~/elasticsearch-backup/

sudo git init
sudo git add .
sudo git commit -m "mohan_nehil_gcloud_2"
sudo git remote add origin https://github.com/Mohankumariitm/gcloud_elk_backup.git
sudo git push origin master





PUT /_snapshot/my_backup/snapshot_1/_restore?wait_for_completion=true








