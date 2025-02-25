#CS320 #Python #Flask

Basics
- Computer sends request to IP address
- Ports are like specific "rooms" in the computer
- you can open and close ports and block with firewalls
- Installing a program like Jupyter will listen for a local port 2020
- python3 -m http.server will launch a locally hosted server
	- found at external_ip:8000

## Flask
- flask.Flask("webapp name") creates a web application
- @something is a decorator
- @app.route("/") runs a function at the given url
- returning a string containing an html file will allow the webapp to display from flask
- flask.Response
