knife ssl fetch https://chefserver.wp.wpensar.com.br


Adicionar em ~/.berkshelf/config.json
{
  "ssl": {
    "verify": false
  }
}

~~~~
export DOMAIN=XXX.XXX.XXX.XX;
~~~~
Copiar chave de criptografia
~~~~
scp -i ~/.ssh/EMorethSP.pem  ~/www/chef-repo/.chef/encrypted_data_bag_secret ubuntu@interno:~/
~~~~


Bootstrap
~~~~
ssh -i ~/.ssh/EMorethSP.pem ubuntu@interno "sudo mkdir -p /etc/chef && sudo mv ./encrypted_data_bag_secret /etc/chef/"

knife bootstrap $DOMAIN --node-name wpensar_interno_apps --ssh-user ubuntu --run-list basic_machine --sudo -i ~/.ssh/EMorethSP.pem -E staging

knife bootstrap FQDN_or_IP_ADDRESS --node-name NAME --ssh-user USERNAME --run-list RUN_LIST --environment ENVIRONMENT --sudo
~~~~

Jenkins
~~~~
https://github.com/zts/cooking-with-jenkins/blob/master/recipes/configure-jenkins.rb
