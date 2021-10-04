# docker
#multiple docker image push to docker repo
set -x
#!/bin/bash
export REMOTE_REG='<Docker_Image_Repo_hub>'
export image_path='<Local_Image_dir_path>' #path in ur setup where all docker images are kept
for img in $(ls -lh $image_path |awk '{print $9}')
do
export NAME=`sudo docker load -i $image_path/$img | tail -1 | awk '{print $3}'`
sudo docker tag $NAME $REMOTE_REG/$NAME
sudo docker push $REMOTE_REG/$NAME
done
