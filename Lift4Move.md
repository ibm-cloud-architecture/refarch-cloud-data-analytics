# Move Data to the Cloud using the Bluemix Lift CLI

**Go Back** to the VM Image.  

1. **Enter** the command **cd $DATA**. This is where the script is that contains all of the Lift CLI command that you will execute to move the data from on-premises to your dashDB database in the cloud.

<img src="./media/vmimage/vmimage-image-15.png"/>

2. **Enter** the command **ls -la**.

<img src="./media/vmimage/vmimage-image-16.png"/>

3. **Enter** the command **vi lift.pf** to edit the Lift properties file.

<img src="./media/vmimage/vmimage-image-17.png"/>

> **Note -** 
>
> The content in the **lift.pf** properties file is case sensitive. Make sure that when you change values noted below that you keep the values in lowercase or Uppercase. For instance, the **target-user** is in lowercase but the **target-schema** is in Uppercase. Keep them in the same case when doing changes.
>

4. **Change** the **target-user**, **target-password** , **target-host** and **target-schema** to your dashDB user, password, host and schema (your schema is the same as your user but in Uppercase...) using the credentials from your dashDB for Analytics service Credentials section you obtained in a previous section.

> **Note -** 
>
> While in the vi editor you can use the arrow keys to move to the character that you want to change and press R to overwrite the character at the cursor location, continue typing with your edits and hit ESC when done to return to command mode.
>

5. **When finished**, hit ESC, hold `SHIFT` and type `ZZ` to save and close the file.

<a name="secgwid" /> 



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
