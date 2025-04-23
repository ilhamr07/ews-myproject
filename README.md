setting devops mini project menggunakan aws

- Membuat service EC2
 konfigurasi : 
 HTTP
 SSH

-connect ke instance via SSH
 di bash
  chmod 400 nama-key.pem
  ssh -i nama-key.pem ec2-user@IP_PUBLIC_EC2

- setelah terhubung ke ec2 melalui ssh instal apache web server

	sudo yum update -y
	sudo yum install -y httpd
	sudo systemctl start httpd
	sudo systemctl enable httpd

cek akses di browser  pakai ip publik

upload file dari local ke aws ec2 dulu menggunakan perintah

scp -i /path/to/my-ec2-keypair.pem index.html ec2-user@<IP_PUBLIC_EC2>:/home/ec2-user/
scp -i /path/to/my-ec2-keypair.pem style.css ec2-user@<IP_PUBLIC_EC2>:/home/ec2-user/

	
upload file index.html dan syle.css ke  /var/www/html/ di EC2
	sudo cp index.html /var/www/html/
	sudo cp style.css /var/www/html/

silahkan akses web dengan http://ip_publik

tahap menjalankan file html di aws ec2 selesai

selanjutnya mencoba  integrasikan dengan github
agar tidak harus upload file manual ketika ada update

instal git di aws ec2

sudo yum update -y
sudo yum install git -y
git --version

sekarang pindah ke github
	buat repository baru
	upload file index.html dan syle.css tadi ke repository dengan perintah diterminal
		cd folder-webmu
		git init
		git remote add origin https://github.com/username/my-website.git
		git add .
		git commit -m "Initial commit"
		git push -u origin master

ssh ke ec2 & clone repository
jalankan di ec2 aws
	cd /home/ec2-user/
	git clone https://github.com/username/my-website.git

akses dengan ippublik apakah berhasil

horee selamat kalau berhasil

untuk test selanjutnya, ubah warna / kata / font yang ada di html dan css
lalu kemudia push ulang ke github
    git add . 
    git commit -m "pesan komit"
    git status
    git push origin main

lalu pindah ke aws ec2 jalankan perintah berikut
    cd /home/ec2-user/<nama file>
    git pull
    sudo cp -r * /var/www/html/

akses dengan ippublik apakah berhasil

