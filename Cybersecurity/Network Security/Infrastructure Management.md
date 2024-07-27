# Backup and Restore Configurations:

## Commands:
    
    copy running-config startup-config: Saves the current configuration to the startup configuration.
    
    copy startup-config running-config: Loads the startup configuration to the running configuration.
    
    copy running-config tftp: Copies the running configuration to a TFTP server.
    
    copy tftp running-config: Loads the configuration from a TFTP server to the running configuration.

# Managing IOS Files:

## Commands:

    copy tftp flash: Copies an IOS image from a TFTP server to the flash memory.
    
    show flash: Displays the contents of the flash memory.
    
    delete flash:[filename]: Deletes a file from the flash memory.
    
    boot system flash:[filename]: Specifies the IOS image file to boot from.
