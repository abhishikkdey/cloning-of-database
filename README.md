# cloning of database

# change clone database name from orclc to whale. replace all name 'orclc' with 'whale'

# configure and start listener_4

<img width="954" height="478" alt="image" src="https://github.com/user-attachments/assets/75082195-bc32-4ed3-8aeb-f4b8d5be376d" />

# copy pasword file

'scp orapworcl_clone oracle@192.168.21.193:/u01/app/oracle/product/19.0.0/dbhome_1/dbs'

# copy pfile

'scp initorcl.ora oracle@192.168.21.193:/u01/app/oracle/product/19.0.0/dbhome_1/dbs'
'vi initorcl_clone.ora'
*.db_name='orcl'

# configure tns
set environment . oraenv

netmgr
<img width="805" height="480" alt="image" src="https://github.com/user-attachments/assets/73c7525d-ec83-4432-9463-21abd8186dab" />

tnsping orcl_clone

<img width="747" height="300" alt="image" src="https://github.com/user-attachments/assets/d0d3bf2b-0a0f-4429-96e2-264574804101" />

<img width="734" height="186" alt="image" src="https://github.com/user-attachments/assets/d83cb03a-b67c-4ad8-b4df-7ecb539b8a72" />
'!rman target sys/oracle@whale'

'connect auxiliary sys/oracle'

<img width="770" height="136" alt="image" src="https://github.com/user-attachments/assets/158a0605-1a0a-4741-8d85-d8f36a428ae8" />

'RMAN> RUN {
DUPLICATE DATABASE TO WHALE FROM ACTIVE DATABASE
SPFILE
PARAMETER_VALUE_CONVERT ('ORCL','WHALE')
SET DB_UNIQUE_NAME='WHALE'
SET DB_FILE_NAME_CONVERT='/u01/app/oracle/oradata/orcl/','/u01/app/oracle/oradata/whale/'
SET LOG_FILE_NAME_CONVERT='/u01/app/oracle/oradata/orcl/','/u01/app/oracle/oradata/whale/'
SET CONTROL_FILES='/u01/app/oracle/oradata/whale/control01.ctl','/u01/app/oracle/fast_recovery_area/whale/control02.ctl'
NOFILENAMECHECK;
}
'



