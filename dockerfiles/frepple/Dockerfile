FROM ubuntu:16.04
RUN apt-get -y -q update
RUN apt-get -y -q upgrade

# RUN apt-get install -y software-properties-common wget
# RUN add-apt-repository "deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main"
# RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
# RUN apt-get update
# RUN apt-get -y install postgresql-9.6
# RUN su - postgres

# RUN psql template1 -c "create user frepple with password 'frepple'"
# RUN psql template1 -c "create database frepple encoding 'utf-8' owner frepple"
# RUN psql template1 -c "create database scenario1 encoding 'utf-8' owner frepple"
# RUN psql template1 -c "create database scenario2 encoding 'utf-8' owner frepple"
# RUN psql template1 -c "create database scenario3 encoding 'utf-8' owner frepple"
# RUN exit

# RUN sed -i 's/local\(\s*\)all\(\s*\)all\(\s*\)peer/local\1all\2all\3\md5/g' /etc/postgresql/9.*/main/pg_hba.conf
# RUN service postgresql restart

ADD resources/ /resources 
WORKDIR /resources

RUN apt-get -y install python3 python3-pip
RUN pip3 install -r requirements.txt

RUN dpkg -i frepple_*.deb
RUN apt-get -f -y -q install

RUN a2enmod expires
RUN a2enmod wsgi
RUN a2enmod ssl
RUN a2ensite default-ssl
RUN a2ensite frepple
RUN service apache2 restart

EXPOSE 8000

ADD start.sh /usr/bin/startfrepple
CMD ["startfrepple"]