Old habits die hard. I still use Windows as the primary OS for my development workflow. Whenever I was interested to any tool exclusive to Linux or Mac OS, I tried to find a windows alternative.

In this case, the tool of interest was Zsh terminal. The default appearance of PowerShell is quite boring and I wanted to give my shell terminal a little visual flair. I was really impressed with Zsh terminal and what it could look like with the help of Oh my Zsh. So I took that as an inspiration and began my quest for a decent Windows/Cross platform alternative.

Along came Starship - a Rust powered, highly customizable and easy to use cross-shell platform.

Here's how I did it -

1) Installing a nerd font
We have to install and enable a nerd font in the terminal. You can choose any font from the list. I used "MesloLGS NF".

2) Installing starship using scoop
>scoop install starship


If you do not have scoop installed, run the following command in your PowerShell to install it -
>iwr -useb get.scoop.sh | iex

Note: if you get an error you might need to change the execution policy with >Set-ExecutionPolicy RemoteSigned -scope CurrentUser

3) Running starship on PowerShell startup

We will have to initiate starship each time a PowerShell instance starts. We can achieve this by adding the following to the end of Microsoft.PowerShell_profile.ps1:

>Invoke-Expression (&starship init powershell)

You can check the location of this file by querying the >$PROFILE variable in PowerShell. Typically the path is ~\Documents\PowerShell\Microsoft.PowerShell_profile.ps1

4) Refreshing the PowerShell session
Enter the following command to refresh the current PowerShell session

>. $profile

Voila!!! You can see its working. Now, on to the fun part which is configuring.

5) Configuration
First from the PowerShell you can type the following command to create the .config directory and a starship.toml file for the configuration.

>New-Item -ItemType Directory -Force ~/.config;New-Item -ItemType file ~/.config/starship.toml;
or if you like to use git bash, you may use the following command -
>mkdir -p ~/.config && touch ~/.config/starship.toml
you will find the newly created directory and config file at the user's home directory, e.g. C:\Users<UserName>

Open the file with your preferred editor and start playing with the configuration.

Pro Tip: you can just run these commands if you want to open the starship.toml file with Visual Studio Code :
>cd  ~/.config;code starship.toml

Here's my preset -
 - This will show the correct icon when a nerd font will be enabled

>command_timeout = 500
>format = "$directory$git_branch$time$cmd_duration$character"
>[line_break]
>disabled = true

>[character]
>success_symbol = "[➜](bold green) "
>error_symbol = "[✗](bold red) "

>[cmd_duration]
>min_time = 500
>format = "took [$duration](bold yellow) "

>[directory]
>read_only = " "
>truncation_length = 3
>truncation_symbol = "~/"

>[git_branch]
>symbol = "  "
>style = "bold #e8ec00 inverted"
>format = "on [$symbol$branch ]($style) "

>[time]
>disabled = false
>format = '[ 🕙 $time ]($style) '
>time_format = "%I:%M:%S %p"
>utc_time_offset = "+6"
>style = "bold bg:#8a15e2"

>[git_commit]
>disabled = true

>[git_state]
>disabled = true

>[git_status]
>disabled = true

>[package]
>disabled = true

That's pretty much it. If you face any issue with installation, feel free to drop a comment. I would be happy to help
