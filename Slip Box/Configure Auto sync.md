
# Prerequisite:

pc and mob
1) The system must be ubuntu, linux
2)  git must be installed  ( apt install git )

mob 
1) termux installed 
2) install openssh and git
3) Also install cron



-----

## Set path to directory
git config --global --add safe.directory /mnt/c/Slip-box-Notes

-----

## Set Remote Repository with the token link access:

git remote set-url origin https://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@github.com/purushottam55/Slip-box-Notes.git

----
## Configure Name and email for remote update : 

git config --global user.name "Purushottam N"
git config --global user.email pnsocialacc@gmail.com

----
## put the following line to crontab -e :

*/1 * * * * cd /mnt/c/Slip-box-Notes && /usr/bin/git pull origin main && /usr/bin/git add . && /usr/bin/git commit -m "Auto-sync $(date '+\%Y-\%m-\%d \%H:\%M:\%S')" && /usr/bin/git push origin main >> /mnt/c/Slip-box-Notes/cron.log 2>&1


---

