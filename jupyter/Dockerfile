FROM ubuntu:16.04


ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get -yq upgrade && \
  apt-get install -yq --no-install-recommends \
  locales wget git nano \
  build-essential python3-pip && \
  apt-get clean &&\
  rm -rf /var/lib/apt/lists/*

RUN localedef -i ja_JP -c -f UTF-8 -A /usr/share/locale/locale.alias ja_JP.utf8
ENV LANG ja_JP.utf8

RUN pip3 install --upgrade pip==9.0.3
RUN pip3 --no-cache-dir install setuptools numpy matplotlib
RUN pip3 --no-cache-dir install jupyter


USER root
EXPOSE 8888

# -- Set up Jupyter Notebook config
ENV CONFIG_JUPYTER /root/.jupyter/jupyter_notebook_config.py
ENV CONFIG_IPYTHON /root/.ipython/profile_default/ipython_config.py 

RUN jupyter notebook --generate-config --allow-root && \
    ipython profile create

RUN echo "c.NotebookApp.ip = '*'" >>${CONFIG_JUPYTER} && \
    echo "c.NotebookApp.open_browser = False" >>${CONFIG_JUPYTER} && \
    echo "c.NotebookApp.iopub_data_rate_limit=10000000000" >>${CONFIG_JUPYTER} && \
    echo "c.MultiKernelManager.default_kernel_name = 'python3'" >>${CONFIG_JUPYTER} && \
    echo "c.NotebookApp.port = 8888" >>${CONFIG_JUPYTER}

RUN echo "c.InteractiveShellApp.exec_lines = ['%matplotlib inline']" >>${CONFIG_IPYTHON} 

WORKDIR /notebooks


# docker build . -t jupyter
# docker run -p 8888:8888 -v /c/docker/notebooks:/notebooks -it jupyter /bin/bash
# jupyter notebook --allow-root

