# simple-html-with-ec2-id-and-image-bmw

to install apache server on an instance via userdata:

user data:

```bash
#!/bin/bash
yum install httpd git -y
firewall-cmd --permanent --add-service=http
firewall-cmd --reload
systemctl start httpd
systemctl enable httpd
systemctl status httpd
rm -rf /var/www/html/bmw
mkdir -p /var/www/html/bmw
chown ec2-user:ec2-user /var/www/html/bmw
chmod -R o+r /var/www/html/bmw
git clone https://github.com/zonender/simple-html-with-ec2-id-and-image-bmw.git /var/www/html/bmw
ec2id=$(curl http://169.254.169.254/latest/meta-data/instance-id)
ec2ip=$(curl http://169.254.169.254/latest/meta-data/local-ipv4)
sed -i "s/ec2id/$ec2id/g" /var/www/html/bmw/index.html
sed -i "s/ec2ip/$ec2ip/g" /var/www/html/bmw/index.html
```

To run it from the command line directly:

```
sudo yum install httpd git -y
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --reload
sudo systemctl start httpd
sudo systemctl enable httpd
sudo systemctl status httpd
sudo rm -rf /var/www/html/bmw
sudo mkdir -p /var/www/html/bmw
sudo chown ec2-user:ec2-user /var/www/html/bmw
sudo chmod -R o+r /var/www/html/bmw
sudo git clone https://github.com/zonender/simple-html-with-ec2-id-and-image-bmw.git /var/www/html/bmw
ec2id=$(curl http://169.254.169.254/latest/meta-data/instance-id)
ec2ip=$(curl http://169.254.169.254/latest/meta-data/local-ipv4)
sudo sed -i "s/ec2id/$ec2id/g" /var/www/html/bmw/index.html
sudo sed -i "s/ec2ip/$ec2ip/g" /var/www/html/bmw/index.html
```
