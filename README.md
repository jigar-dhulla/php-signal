# php-signal

php-signal is a slim PHP wrapper around [signal-cli](https://github.com/AsamK/signal-cli)

## Features:

- Send messages to individuals, groups.
- Link to Master Device (Smartphone)
- Manage Groups
- Manage Profile
- Manage Device
- Receive Messages (Not as Daemon)
- Check if Number exist on Signal Server
- Register, Verify and Unregister Number

## How to Install signal-cli

Please refer official [Installation Doc](https://github.com/AsamK/signal-cli#installation)

**Note**: Please make sure to keep .so|.dylib library in same directory as the binary
## Installation

    composer require jigarakatidus/php-signal

## Usage

    require 'vendor/autoload.php';
    
    use jigarakatidus\Signal;
    
    $client = new Signal(
        '/Users/jigar.d/signal-cli/bin/signal-cli', // Binary Path
        '+919664*****', // Username/Number including Country Code with '+' 
        Signal::FORMAT_JSON // Format
    );
    
    // Register the Number (username)
    $client->register()

    // Verify the Number
    $client->verify('112-360');

    // Unregister the Number
    $client->unregister();

    // Check if number(s) exist on Signal Server
    $client->getUserStatus(['+91966xxxxxxx', '+91961xxxxxxx']);
    
    // Send Message
    $client->send(['+91966xxxxxxx', '+91961xxxxxxx'], "Hi, testing from' PHP Library");
    
    // Receive Messages - More details in DocBlock
    $client->receive();

    // Update Name, Avatar, etc
    $client->updateProfile('Jigar D');

    // Link this signal-cli as secondary device
    $client->link('MacBook');

    // Link other devices to this one.
    // Works only when this is master
    $client->addDevice('tsdevice:/?uuid=6dNLUdpVTdCV-q_eN6TJtA&pub_key=BUCL9Jq64r1yLvNeyzS0mJgMjz2u82he3B5Wr%2BtrMitx');

    // List Devices
    $client->listDevices();
    
    // Remove Device, works only when this is master
    $client->removeDevice(2);

    // Update the account attributes on the signal server
    $client->updateAccount();

    // Create Group
    $client->createGroup('Test', ['+91961xxxxxxx']);

    // List Groups
    $client->listGroups();

    // Join Group
    $client->joinGroup('https://signal.group/#CjQKIEBNZJkVK5IMtoQZt46O-ZIdhOqeQCwtrZQsag_3FUoIEhBrN_ht_mr6Dbe5vR-EWpVm');

    // Quit Group
    $client->quitGroup('usPpOsVTgDTt8JE8UKedMhYXteL2YE5WzYzMnJEp/gI=');

## Output and Error
More details from command can be fetched. eg:

    $client->getCommand()->getOutput();
    $client->getCommand()->getError();
    $client->getCommand()->getExitCode();

## Testing
- This works with [signal-cli 0.9.2](https://github.com/AsamK/signal-cli/releases/tag/v0.9.2)
- Tested on PHP 7.3

## TODO
- Unit Tests
- Better handling to link to a device

## License

This project uses 
- [signal-cli](https://github.com/AsamK/signal-cli)
- [mikehaertl/php-shellcommand](https://github.com/mikehaertl/php-shellcommand)

Licensed under the GPLv3: http://www.gnu.org/licenses/gpl-3.0.html
