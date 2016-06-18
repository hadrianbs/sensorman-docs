========
Usage
========
To use the web app, you have to register , then register a sensor.
Register an account at http://sensorman.bayanulhaq.me/authentication/register

Then register a sensor. After you registered your sensor, you'll get a sensor key like this ::

	cb3e705e318dafc74a95ca4c725c249b63bbadc8

After that, you can code your device (a raspberry pi, a computer, an arduino, or anything you can think off.)

The data collection API is located at ::

	http://sensorman.bayanulhaq.me/send-data

The data collection api uses HTTP Post method with JSON data format. It means you have to encapsulate the data you'll send from your sensor as JSON. The data that the API retrieve is "sensor_key" and "sensor_reading".
Here's an example::

	{"sensor_key": "4112f06300ff3c0da70186c16ee6f229fa6cb126", "sensor_reading": 24.64791526016068}

"sensor_key" is the sensor key you got when registering a sensor.
"sensor_reading" is the actual sensor reading.

Here's an example client with python. It sends random value per n second. You can set the delay beetween sending the data::

	import socket
	import time
	import json
	import urllib2
	import random



	def sendSensorData():


		sensor_key = '4112f06300ff3c0da70186c16ee6f229fa6cb126'
		sensor_reading = random.uniform(81, 87)


		data = 	{
			'sensor_key': sensor_key,
			'sensor_reading': sensor_reading
		}

		req = urllib2.Request('http://192.168.1.114/sensorman/api/retrieve_data/')
		req.add_header('Content-Type', 'application/json')
		response = urllib2.urlopen(req, json.dumps(data))
		print json.dumps(data)
		print response.read()

	while(True):

		sendSensorData()
		time.sleep(2)	



To use this template, simply update it::

	import read-the-docs-template
