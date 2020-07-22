# Trick-DL

### CelebA dataset
```
cat img_celeba.7z.0** > img_celeba.7z

7z x img_celeba.7z
```

### Json File
```
import json
class NumpyEncoder(json.JSONEncoder):
    """ Special json encoder for numpy types """
    def default(self, obj):
        if isinstance(obj, (np.int_, np.intc, np.intp, np.int8,
            np.int16, np.int32, np.int64, np.uint8,
            np.uint16, np.uint32, np.uint64)):
            return int(obj)
        elif isinstance(obj, (np.float_, np.float16, np.float32, 
            np.float64)):
            return float(obj)
        elif isinstance(obj,(np.ndarray,)): #### This is the fix
            return obj.tolist()
        return json.JSONEncoder.default(self, obj) 
    
def save_to_json(dic,target_dir):
    dumped = json.dumps(dic, cls=NumpyEncoder)  
    file = open(target_dir, 'w')  
    json.dump(dumped, file)
    file.close()
    
def read_from_json(target_dir):
    f = open(target_dir,'r')
    data = json.load(f)
    data = json.loads(data)
    f.close()
    return data 
```

### Make Dir

```
try:
    os.makedirs(audio_path)
except OSError:
    pass
```
