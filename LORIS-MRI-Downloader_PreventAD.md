
# Prevent AD MRI scans downloader


```python
import getpass  # For input prompt not to show what is entered
import json     # Provide convinent functions to handle json objects 
import requests # To handle http requests
import os 

hostname = 'openpreventad.loris.ca'
baseurl = 'https://' + hostname + '/api/v0.0.3-dev'
```

### Login procedure


```python
print('Login on ' + hostname)

payload = {
    'username': input('username: '), 
    'password': getpass.getpass('password: ')
}

response = requests.post(
    url = baseurl + '/login',
    json = payload,
    verify = True
)

text = response.content.decode('ascii')

if (response.status_code == 200):
    token = json.loads(text)['token']
    print('login successfull')
else:
    print(text)

```

### Extraction


```python
candidates = json.loads(requests.get(
    url = baseurl + '/candidates/',
    verify = False,
    headers = {'Authorization': 'Bearer %s' % token}
).content.decode('ascii'))

for candidate in candidates['Candidates']:
    candid = candidate['CandID']
    sessions = json.loads(requests.get(
        url = baseurl + '/candidates/' + candid,
        verify = False,
        headers = {'Authorization': 'Bearer %s' % token}
    ).content.decode('ascii'))
    
    for visit in sessions['Visits']:
        
        directory = candid + '/' + visit
        try:
            os.makedirs(directory)
        except FileExistsError:
            pass
        
        session = json.loads(requests.get(
            url = baseurl + '/candidates/' + candid + '/' + visit,
            verify = False,
            headers = {'Authorization': 'Bearer %s' % token}
        ).content.decode('ascii'))
        
        sessionmetafile = open(directory + '/session.json', "w")
        sessionmetafile.write(str(session['Meta']))
        sessionmetafile.close()
            
        files = json.loads(requests.get(
            url = baseurl + '/candidates/' + candid + '/' + visit + '/images',
            verify = False,
            headers = {'Authorization': 'Bearer %s' % token}
        ).content.decode('ascii'))
        
        for file in files['Files']:
            filename = file['Filename']
            relativepath = directory + '/' + filename
            
            if not os.path.isfile(relativepath):
                image = requests.get(
                    url = baseurl + '/candidates/' + candid + '/' + visit + '/images/' + filename,
                    verify = False,
                    headers = {'Authorization': 'Bearer %s' % token}
                )
                mincfile = open(relativepath, "w+b")
                mincfile.write(bytes(image.content))
            
            relativepath = directory + '/' + filename + '.qc.json'
            if not os.path.isfile(relativepath):
                qc = requests.get(
                    url = baseurl + '/candidates/' + candid + '/' + visit + '/images/' + filename + '/qc',
                    verify = False,
                    headers = {'Authorization': 'Bearer %s' % token}
                )
                qcfile = open(relativepath, "w+b")
                qcfile.write(bytes(qc.content))
            
        

```


```python

```
