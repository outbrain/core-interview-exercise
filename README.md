# Core Services Exercise
Please read the following instructions before starting to implement your exercise, you don't want to miss any important instruction.

### Creating your repository 

Please mirror this git repo using the instructions [here](https://help.github.com/articles/duplicating-a-repository). Then clone it locally. 
(**Please DO NOT fork the repo**)

### Submitting your solution

You may use one of the following coding languages: Python/Ruby.

The exercise should be delivered as a GitHub repository in your private account, containing:
1. Directory with all the modules of your service (providing a clear directory tree is an advantage).
2. Dockerfile that runs the web framwork and copies the code to the container.
3. Basic instructions on how to use the Dockerfile and examples for querying the service.

Requirments:
1. The service should be started by the Dockerfile and should print all logs/output to the container's shell.

Nice to have:
1. Pay attention to your code structure and organization in classes, functions and modules. Naming convention will also be taken into consideration.
2. We will be looking at you commit history. A tidy commit history is an advantage.


### Exercise
Write a small API service that will expose the following routes:

~~~
/v1/api/checkCurrentWeather
/v1/api/checkCityWeather?city=Tel-aviv
/v1/api/driveStatus?status=Offline
~~~

#### checkCurrentWeather
This endpoint will check your location according to your IP, then check the current weather at your location and return the result in following format:
`{"city": <city>, "country": <country>, "degrees": <degrees>}`

* Degrees should be shown in Celsius.
* You can get the location according to the IP via this service: http://ipinfo.io/ 
* You can fetch the weather information for a given location via this service: https://openweathermap.org/current. We will provide you with an API key.

##### Response example

~~~
{"city": "Tel-Aviv", "country": "IL", "degrees": 30}
~~~

#### checkCityWeather
This endpoint will check the current weather at a specific location passed as a query parameter, and will return the result in the following format:
`{"city": <city>, "country": <country>, "degrees": <degrees>}`

* Degrees should be shown in Celsius.
* You can fetch the weather information for a given location via this service: https://openweathermap.org/current. We will provide you with an API key.

##### Response example

~~~
{"city": "Haifa", "country": "IL", "degrees": 26}
~~~

#### driveStatus
This endpoint will receive as body the data defined in [input.json](https://github.com/outbrain/core-interview-exercise/blob/new_exercise/input.json), and will parse the data to return only the drives in the provided status (defined as a query parameter).

##### Response example

```
{
  "message": "Found 1 offline drives",
  "data": [
    {
      "name": "SP4",
      "size": "4764771 MB",
      "free": "2333948 MB",
      "path": "/dev/sdk",
      "log": "0 MB",
      "port": 5660,
      "guid": "db53cc9f02524622005b30b0eb0947e3",
      "clusterUuid": "-8650609094877646407--116798096584060989",
      "disks": ["/dev/sdk", "/dev/sdl", "/dev/sdm"],
      "dare": 0
    }
  ]
```

* In cases where the value of the `status` query param is not found in the body, return a proper message and an empty data list.
* In the input file, each key is a drive and each value is a string representing the drive's information.
