# Quality Assurance

---

## Specifications

Before the start of the project, it is mandatory to complete a specifications document. 
This document will list all mandatory and optional features (or by priority).
Objectives should be SMART.

- Specific
- Measurable (can also be OK / NOK)
- Accepted
- Realistic
- Scheduled

Specifications can also be changed or appended. 
It is important to have a document with test criteria according to which a product or the software can be tested and evaluated.
In the specification, someone (the developer) thinks about how they would prefer the product to work e.g. menus, interactive elements, GUI, HMI, etc. 

## Unit tests

(todo)


## Continuous Integration (CI/CD)

CI/CD is a concept from the software industry.
It can be applied to Embedded Systems as well.
One of the simplest test for an embedded project is a remote auto-build on a (Jenkins-) server.

The server could in theory run the firmware tests, if there are any.
Using `st-flash` the server could upload new binaries to a devboard attached to the server directly.

Given successfull testing an new git tags / releases, the server could then also automatically distribute the new firmware.
A distribution recipient could be the company's production line (e.g. a network drive, or an email to the head of production).
Another recipient could be the company's website where customers can download firmware binaries to upgrade their devices.

### Configuring Jenkins (Server Side - DevOps)

(todo)

### Configuring Jenkins (Developer Side - Project)

(todo)

```bash
sudo apt install gcc-arm-none-eabi
```

#### Execute Shell Script

```bash
echo "Tool versions"
python --version
arm-none-eabi-gcc --version
# st-flash --version

echo "Updating submodules ..."
git submodule update --init

echo "Converting MAKEFILE ..."
python makefile-fix.py

echo "Starting build using arm-none-eabi-gcc ..."
cd $WORKSPACE/Debug
pwd
make all

echo "Done!"

# echo "Uploading to Device under Test ..."
# echo "st-flash Version:"
# st-flash write Debug/f303re_Voltmeter.bin 0x08000000
# echo "Done!"
```

#### Make your Project compile without the IDE

The standard project is developed on STM32CubeIDE on a Windows machine.
The makefile therefore uses Windows paths which do not work on a Linux auto-build host.
A python script can be run by the auto-build host to convert the makefile paths automatically.

`convert-makefile.py`

```python
#!/usr/bin/python3
import os
makefile = './Debug/makefile'  # or ./Release/makefile

rf = open(makefile)
temp = ''
for line in rf:
	pattern = ''
	if('Users' in str(line)):
		lin = str(line).replace('\n','').split(' ')
		for arg in lin:
			if('Users' in arg):
				pattern = arg
				arg = arg.split('\\')
				nln = arg[0].split('C:')[0] + '../' +  arg[-1]
	if(len(pattern) > 1):
		line = line.replace(pattern, nln)
	temp += line
rf.close()

os.remove(makefile)

wf = open(makefile, 'w')
wf.write(temp)
wf.close()
```




