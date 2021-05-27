### Desafio Twin Towers

Desafio twin towers recuperar block storage EC2.
Recuperar instancia EC2 sem precisar instalar do zero.
Corrompa o root de uma instancia EC2
Restaurar corrompido (snapshot)

##Solucao
#1 Criar um snapshot
```yml
aws ec2 create-snapshot --volume-id <volume-id> --description 'Desafio Twin Towers' --tag-specifications 'ResourceType=snapshot,Tags=[{Key=purpose,Value=desafiotwintowers},{Key=costcenter,Value=tcbmodulo3}]'
snap-0b1e6f2f992ac4c46
```
#2 Conferir se o snapshots foi criado com sucesso
```yml
aws ec2 describe-snapshots --owner-ids self  --query 'Snapshots[]' --region=us-east-1
```

#3 Caso alguma falha ocorra (“corrompa o root volume”) com a instância EC2
```yml
aws ec2 create-replace-root-volume-task --instance-id <instance-id> --snapshot-id <snapshot-id>
```

##FAQ
1. Onde eu encontro o <instance-id> e <volume-id>?
```yml
aws ec2 describe-instances --query 'Reservations[*].Instances[*].{Id:InstanceId,Pub:PublicIpAddress,Pri:PrivateIpAddress,State:State.Name,VolumeId:BlockDeviceMappings[0].Ebs.VolumeId}' --output table
```
2. Onde eu encontro o <snapshot-id>?
```yml
aws ec2 describe-snapshots --owner-ids self  --query 'Snapshots[]' --region=us-east-1 --output table
```
---------------------------------------
##Plus

#Delete snapshot
```yml
aws ec2 delete-snapshot --snapshot-id 
```
#Delete volume
```yml
aws ec2 delete-volume --volume-id
```
*Live :v:
*Love :heart:
*Learn :see_no_evil: :hear_no_evil: :speak_no_evil:

:rocket::rocket::rocket:
*ansible
*aws
*iam
*pracima 
*thecloudbootcamp
