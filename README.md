# pypi_server

Instructions on how to build a python package distro and then serve and install the package from a private pypi server.
In this repo, `math_operations` is a custom python module, which is built, then served with a localhost pypi and installed in a virtual environment.

## Build the distro files

1. ```python -m pip install --upgrade build```
2. ```cd math_operations```
3. ```python -m build```
4. ```python -m venv venv```
   ```venv\Scripts\activate```
5. ```cd math_operations```
   ```pip install dist/math_operations-0.1.0.tar.gz```
6. ```cd ..```
   ```python test.py```

## Run the pypiserver

1. ```pip install pypiserver```  
2. ```mkdir ~/packages```
3. Check the actual path (windows): ```Resolve-Path ~/packages``` 
   i.e: C:\Users\Ian\packages
4. copy your package to `~/packages` location, including the folder name with both .tar.gz and .whl.
5. ```pypi-server run -p 3001 ~/packages```
6. from the client run the following command:
   ```pip install --extra-index-url http://localhost:3001/simple/ math_operations```

File Structure Map:

```
pypiserver_project/
├── packages/                    # Directory where package files are stored
│   ├── package_name1/
│   │   ├── package_name1-0.1.0-py3-none-any.whl
│   │   ├── package_name1-0.1.0.tar.gz
│   ├── package_name2/
│   │   ├── package_name2-1.0.0-py3-none-any.whl
│   │   ├── package_name2-1.0.0.tar.gz
├── .htpasswd                   # (Optional) File for HTTP basic authentication
├── config.ini                  # (Optional) Configuration file for pypiserver
├── simple/                     # (Auto-generated) Directory for PEP 503 simple API
│   ├── package_name1/
│   │   ├── index.html         # Metadata for package_name1
│   ├── package_name2/
│   │   ├── index.html         # Metadata for package_name2
└── Dockerfile                  # (Optional) For containerized deployment
```