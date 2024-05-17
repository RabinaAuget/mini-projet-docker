#API Image gave by POZOS
FROM python:3.8-buster

#Maintainer specification
LABEL maintainer="Rabina AUGET"

#Needed packages installation
RUN DEBIAN_FRONTEND=noninteractive apt -o Acquire::Check-Valid-Until=false update --allow-releaseinfo-change -y && apt install python-dev python3-dev libsasl2-dev python-dev libldap2-dev libssl-dev -y && apt clean -y

#COPY API requirement file
COPY requirements.txt student_age.py  /

#Installation launch & clean the temp directory after the installation
RUN pip3 install -r /requirements.txt && rm -rf /root/.cache/pip/*

#Persistent data
VOLUME /data

#API Port
EXPOSE 5000

#running student_age.py
CMD [ "python3", "/student_age.py" ]
