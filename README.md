# dnsrpz
Domain Name Service Response Policy Zones (DNS RPZ)

Berikut adalah kumpulan dari DNS yang telah dihimpun dari email Trust Positif


# INSTALASI:

Requirement:

## BIND 9.10+

Instalasi: 

1. `cd /var/named`
2. `git clone https://github.com/dionipe/dnsrpz`

3. edit file `/var/named/dnsrpz/trustpositif.zone`. Sesuaikan record A dnssehat dengan host sendiri, atau biarkan seperti itu saja.

4. edit named.conf, 

di options:
```
options {
..
..
     response-policy {zone "trustpositif";};
..
..
}
```
tambahkan zone trustpositif di named.conf
```
zone "trustpositif" IN {
        type master;
        file "/var/named/dnsrpz/trustpositif.zone"; #di sesuaikan dengan setting / direktori named
        allow-query {any;};
        allow-update {none;};
};
```

# Untuk Contributor:

Add Record:
```
echo "xx.namadomain.com IN CNAME dnssehat" >> trustpositif02.zone
git commit -q -m "add domain name"
git push -q
```


Delete Record:
```
sed -i '/xx.namadomain.com/d' trustpositif02.zone
```

Apply all command :
```
git commit -q -m "delete record domain.com"
git push -q
```

