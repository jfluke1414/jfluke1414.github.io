---         
order: 5   
title: (GITHUB) github basic   
category: Github   
---         
   
cd /home/crypto/htdocs/crypto   
echo "# Ar_Crypto_Python" >> README.md   
git init   
git add README.md   
git commit -m "first commit"   
git remote add origin https://github.com/jfluke1414/Ar_etcs_python.git   
git push -u origin master   
   
>>project push   
cd /home/crypto/htdocs/crypto   
git add .   
git commit -m "update"   
git push   
   
git config --global user.name "username"   
git config --global user.email user_email   
git config --global user.password "password"   
   
git push -u origin master   
git pull -u origin master   
   
git branch branch_name   
git checkout branch_name   
