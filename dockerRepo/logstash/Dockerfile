ARG ELK_VERSION
FROM logstash:${ELK_VERSION}

USER root
# Add logstash plugin
RUN logstash-plugin install logstash-filter-date_formatter
RUN logstash-plugin install logstash-input-beats

RUN yum -y install centos-release-scl
RUN yum -y install rh-python36
# Add RHSCL Python 3 to my login environment
#RUN /bin/bash -c "source scl_source enable rh-python36" /etc/bashrc
RUN echo "source scl_source enable rh-python36" >> /root/.bashrc
# Install Libraries
RUN /bin/bash --login -c "pip install pyhocon==0.3.54 elasticsearch==7.5.1 jinja2==2.11.1"
#RUN pip install pyhocon==0.3.54 elasticsearch==7.5.1 jinja2==2.11.1 progressbar2
ADD .vimrc /root/.vimrc
RUN mkdir -p /home/logstash/logfile
RUN chown -R logstash:logstash /home/logstash/logfile/

# Folder for --path.data, Hardcoded in LogStashCommand.py
#RUN mkdir -p /var/log/path
# By running tail command overrides the behavious of logstash running in the 
#background
EXPOSE 8088 8081
CMD ["tail","-f","/dev/null"]
