#API Image gave by POZOS
FROM python:3.8-buster

#Maintainer specification
LABEL maintainer="Rabina AUGET"

#Needed packages installation
RUN DEBIAN_FRONTEND=noninteractive apt -o Acquire::Check-Valid-Until=false update --allow-releaseinfo-change -y && apt install python-dev python3-dev libsasl2-dev python-dev libldap2-dev libssl-dev -y

#Persistent data
VOLUME /data

#Code source add from github
RUN git clone https://github.com/diranetafen/student-list.git /data

WORKDIR /data

#copy of the needed package in the requirements.txt
COPY /data/student-list/simple_api/requirements.txt /data/requirements.txt

#API Port
EXPOSE 5000

#Installation launch
RUN pip3 install -r /data/requirements.txt

#running student_age.py
CMD [ "python3", "/data/simple_api/student_age.py" ]