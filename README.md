```python
import threading
import requests
import datetime

def download_images(amount):
	for num in range(amount):
		url = 'http://picsum.photos/id/'+str(num)+'/1920/1080'
		print(url)
		req = requests.get(url,stream=True)
		print(req)
		if req.status_code == 200:

			fname = 'images/'+str(num)+'.png'
			with open(fname,mode='wb') as file:
				for image in req:
					file.write(image)
			print(fname, "downloaded")
start_time = datetime.datetime.now()
print(start_time)
t1 = threading.Thread(target=download_images, args=(100,))
t1.start()
t1.join()
end_time = datetime.datetime.now()
print(end_time-start_time)
```
