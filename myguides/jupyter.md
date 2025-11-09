## setup Jupyter Nodebook ##
sudo apt install python3 python3-pip -y
python3 -m venv jupyter_env
source jupyter_env/bin/activate
pip install notebook
pip install boto3 (to be used inside jupyter, python enviroemnt)

jupyter notebook

http://localhost:8888


deactivate

