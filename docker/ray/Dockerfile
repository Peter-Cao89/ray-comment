ARG BASE_IMAGE
ARG FULL_BASE_IMAGE=rayproject/ray-deps:nightly"$BASE_IMAGE"
FROM $FULL_BASE_IMAGE

ARG WHEEL_PATH
ARG FIND_LINKS_PATH=".whl"
ARG CONSTRAINTS_FILE="requirements_compiled.txt"

COPY requirements_compiled.txt ./
COPY $WHEEL_PATH .
COPY $FIND_LINKS_PATH $FIND_LINKS_PATH

# Required a recent version of setuptools to be compatible with python 3.12+.
RUN $HOME/anaconda3/bin/pip install setuptools==71.1.0

RUN $HOME/anaconda3/bin/pip --no-cache-dir install -c $CONSTRAINTS_FILE \
    `basename $WHEEL_PATH`[all] \
    --find-links $FIND_LINKS_PATH && sudo rm `basename $WHEEL_PATH`

RUN $HOME/anaconda3/bin/pip freeze > /home/ray/pip-freeze.txt
