****full_backup
source /home/oracle/.bash_profile
rman target / log=/home/oracle/backup/backupall_rman.log<<EOF
run
{
allocate channel ch1 device type disk; #分配通道
allocate channel ch2 device type disk;
sql 'alter system archive log current'; #归档当前日志
backup database format '/home/oracle/backup/db_%d_%T_%U';
sql 'alter system archive log current';
backup archivelog all format '/home/oracle/backup/arch_%t_%s' delete all input;
backup format '/home/oracle/backup/con_%s_%p' current controlfile;
crosscheck backup;
crosscheck archivelog all;
delete noprompt expired backup;
delete noprompt obsolete;
delete noprompt backup of database completed before 'sysdate -15';
delete noprompt archivelog all;
delete noprompt backup of archivelog all completed before 'sysdate -15';
release channel ch1;
release channel ch2;
}
EOF
