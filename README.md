# golang_omniosce_build
Instructions to build Golang in OmniosCE

mkdir code
cd code/
pkg install git gcc44 system/header rsync developer/object-file
mkdir /usr/local
git clone https://go.googlesource.com/go
cd go ; git checkout release-branch.go1.4 ; cd src
CC=/opt/gcc-4.4.4/bin/gcc ./all.bash
(Have a coffee)
rsync -az ~/code/go /usr/local/
git checkout -- ..
git clean -df
git checkout release-branch.go1.10
git pull
CC=/opt/gcc-4.4.4/bin/gcc GOROOT_BOOTSTRAP=/usr/local/go ./all.bash
(Have a coffee)
(Tests will fail, it's an issue with old gcc: replace -rdynamic with -export-dynamic)
mv /usr/local/go/ /usr/local/go1.4
mv ~/code/go/ /usr/local/go1.10

root@omniosce:~# /usr/local/go1.10/bin/go version
go version go1.10.1 solaris/amd64

