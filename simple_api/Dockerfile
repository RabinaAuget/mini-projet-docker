#API Image gave by POZOS
FROM python:3.8-buster

#Maintainer specification
LABEL maintainer="Rabina AUGET"

#Needed packages installation
RUN DEBIAN_FRONTEND=noninteractive apt -o Acquire::Check-Valid-Until=false update --allow-releaseinfo-change -y && apt install python-dev python3-dev libsasl2-dev python-dev libldap2-dev libssl-dev -y

#Persistent data
VOLUME /data

#Cleaning the directory before cloning
RUN rm -Rf /data/*

#Definition of the work directory
WORKDIR /data

#Code source add from github
RUN git clone https://github.com/diranetafen/student-list.git

#Installation launch
RUN pip3 install -r /data/student-list/simple_api/requirements.txt

#API Port
EXPOSE 5000

#running student_age.py
CMD [ "python3", "/data/student-list/simple_api/student_age.py" ]
