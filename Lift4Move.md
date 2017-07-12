# Move Data to the Cloud using the Bluemix Lift CLI

**Go Back** to the VM Image. You should be back where you left off in the Lift CLI data directory (/export/home/nz/lift-cli-data. If you are not, **Enter** a command of **cd $DATA**. This is where the script is that contains all of the Lift CLI command that you will execute to move the data from on-premises to your dashDB database in the cloud.

<img src="./media/vmimage/vmimage-image-24.png"/>

1. **Enter** the command **ls -la** to list the directory contents.
2. **Enter** the command **cat lift-to-dashdb | more** to view the Lift script contents.

<img src="./media/vmimage/vmimage-image-25.png"/>

**Scroll** through the script by hitting the space bar on the keyboard until you have viewed the entire script. **Notice** the **lift extrac**, **lift put**, **lift ls** and **lift load** commands and the syntax used to execute them. The Lift commands were put into a script for your convenience so you can execute them all at once instead of individually.

<img src="./media/vmimage/vmimage-image-26.png"/>

3. **Enter** the command **lift-to-dashdb | more** to execute the Lift script and begin moving the data to the cloud.

<img src="./media/vmimage/vmimage-image-27.png"/>

**Scroll** through the output by hitting the space bar on the keyboard until the script is complete.

<img src="./media/vmimage/vmimage-image-28.png"/>

**Notice** the Load record counts. You should have loaded a total of 11,022 rows to the BANK_CUSTOMERS table in dashDB. 3,000 N Bank Customers and 8,022 K Bank Customers.
