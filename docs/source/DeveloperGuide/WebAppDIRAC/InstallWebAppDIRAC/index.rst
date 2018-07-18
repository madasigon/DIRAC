You have already prepared your eclipse. Now you can try to install DIRAC and the Web portal locally. The instruction is given for MAC OS users, but it is similar to Linux users as well. I use different directory for developing WebAppDIRAC than the directory where the portal is installed. I always copy the code from the development area to the installed area in case when I wanted to test it. The next section I will give an instruction about how to install DIRAC and WebAppDIRAC.

Install DIRAC & WebAppDIRAC
###########################
-I propose to read the following documentation and after continue to install DIRAC (https://github.com/DIRACGrid/DIRAC/wiki/GitSetup).

1. Create a directory where you will install DIRAC and WebAppDIRAC: mkdir portal; cd portal

2. **git clone git://github.com/zmathe/DIRAC.git** (NOTE: This works when you forked the DIRAC repository). or execute: **git clone https://github.com/DIRACGrid/DIRAC.git** 

3. **git clone git://github.com/zmathe/WebAppDIRAC.git** (NOTE: This works when you forked the WebAppDIRAC repository on github) or git clone https://github.com/DIRACGrid/WebAppDIRAC.git

4. **./DIRAC/Core/scripts/dirac-install.py -r v6r21-pre1 -X -t server --dirac-os --dirac-os-version=0.0.6** (You can use the current production version of DIRAC which can found http://diracgrid.org. NOTE: The current version of dirac-os is 0.0.6 but this might change. The available versions can be found at http://lhcbproject.web.cern.ch/lhcbproject/dist/Dirac_project/installSource/.)

If DIRAC properly installed, you can continue to install WebAppDIRAC.
NOTE: In case of timeout use: ./DIRAC/Core/scripts/dirac-install.py -r v6r21-pre1 -X -t server --dirac-os --dirac-os-version=0.0.6 -T 600000

5. **python DIRAC/Core/scripts/dirac-deploy-scripts.py**

6. **./WebAppDIRAC/dirac-postInstall.py**

7. **source bashrc** (we have to use the correct python in order to install tornado)

8. **pip install tornado**

9. **mkdir etc**

10. you need to create: **vi etc/dirac.cfg** file For example (It is an LHCb specific configuration. You have to use your Configuration servers):
::

  DIRAC {
   #Setup = LHCb-Production
   Setup = LHCb-Certification
   Configuration {
      Servers = dips://lhcb-conf-dirac.cern.ch:9135/Configuration/Server
   }
   Security {
      CertFile = <location of hostcert.pem>
      KeyFile = <location of hostkey.pem>
   }
   Extensions = WebApp
  }

**NOTE: If you don't want to use Balancer, open WebAppDIRAC/WebApp/web.cfg and uncomment this line: #Balancer = None.**

11. You need the grid-certificates under etc directory. If you do not known about it, please ask the appropriate developer.

12. **python WebAppDIRAC/scripts/dirac-webapp-run.py -ddd**

13. open firefox/safari/chrome… and open the following url: https://localhost:8443/DIRAC
