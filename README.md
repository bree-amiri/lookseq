lookseq
=======

This is a fork of Magnus Manske's lookseq application. See
http://sourceforge.net/projects/lookseq/ for the truth.

Local Installation
------------------

The instructions below are for installation on a local computer
running Ubuntu 12.10 assuming you have sudo.

Install dependencies:

```
apt-get install apache2
cpan Digest::SHA1
cpan JSON
```

Get lookseq:

```
cd /opt
git clone git://github.com/alimanfoo/lookseq.git
chown -R www-data:www-data /opt/lookseq
```

Configure Apache virtual host:

```
cp /opt/lookseq/lookseq.site /etc/apache2/sites-available/lookseq
a2ensite lookseq
echo "127.0.1.1 lookseq" >> /etc/hosts
apache2ctl configtest
apache2ctl restart
```

Test it works: http://lookseq/

To configure for your data, edit /opt/lookseq/cgi-bin/config.json.

Note that the reference sequence (fasta file) will need to have bases
in uppercase. If not, do something like:

```
sed -i -e 's/\([actg]\)/\U\1/g' ref.fa 
```

Also the reference sequence needs to be indexed (samtools faidx) as do
all the BAM files (samtools index).

Note also that the Apache user (usually www-data) will need permission
to read your data files.

If you have any problems, look in /var/log/apache/error.log.