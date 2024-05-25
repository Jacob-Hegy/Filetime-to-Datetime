# Time Converter Script
```python
#!/usr/bin/python3
import argparse
from datetime import *

parser = argparse.ArgumentParser(description = "Convert dwLowDateTime and dwHighDateTime to a UTC timestamp")
parser.add_argument('-x', '--low', help = "dwLowDateTime", type = int, required = True)
parser.add_argument('-y', '--high', help = 'dwHighDateTime', type = int, required = True)

args = parser.parse_args()

EPOCH_FILETIME = 116444736000000000

class Timestamp:
	def __init__(self, ldt, hdt):
		self.dw_ldt = ldt
		self.dw_hdt = hdt

	def getTime(self):
		return datetime.fromtimestamp((((self.dw_hdt << 32) | (self.dw_ldt & 0xFFFFFFFF)) - EPOCH_FILETIME)  / (10 ** 7), timezone.utc)

def main():
	print(Timestamp(args.low, args.high).getTime())

if __name__ == "__main__":
	main()
```
