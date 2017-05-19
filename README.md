# Reddcoin.NET
.NET Library for RPC calls to ReddCoin Wallet

This .NET library is to help with RPC commands for your Reddcoin Wallet.
I have not included the "createrawtransaction" RPC call at this point, but if enough 
people as about it, I'll gladly put it in.  

Usage:

Include the DLL in the reference of your .NET program (ASP.NET, C#, etc...)
You may need to include the Newtonsoft.JSON DLL in your program as well.

Set up your configuration file as follows:

username=<RPC Username>
password=<RPC Password>
ip_addr=<IP address of Wallet>
port=<RPC Port>
nocommand=<command1,command2,...>

The nocommand line indicates which commands are available when using the Library
If you do not want anyone to have the ability to "move" coins using the "move" rpc command
use nocommand=move

If there are multiple RPC commands that you do not want to let anyone have access to use
nocommand=move,createrawtransaction,help

In your main program, set the Load.ConfigLocation string to the path that has your config file in it.
Example:
using ReddCoinNet;
private void OnLoad()
{
	Load.ConfigLocation = "c:\users\<username>\desktop\config.conf";
}

This will allow you to store your file anywhere you need to.

For an ASP.NET website, you can use the following:

 public ActionResult Calls(string id)
{
	dynamic results = string.Empty;
	string data;
	string[] line_results;

	Load.ConfigLocation = HostingEnvironment.MapPath("~/config.conf");
	{
		if (Load.FileData())
		{
			string cmd = string.Empty;
			string[] line_args = new string[1];
			data = id;
			if (data != null)
			{
				line_results = data.Split(' ');
				if (line_results.Length > 0)
				{
					cmd = line_results[0];
					line_args = new string[line_results.Length - 1];
					if (line_results.Length == 1)
					{
						line_args = null;
					}
					else
					{
						for (int x = 0; x < line_args.Length; x++)
						{
							line_args[x] = line_results[x + 1];
						}
					}
					results = Parse.Parse_cmd(cmd, line_args);
				}
				else
				{
				}
			}
			else
				results = "Parameters are missing";
		}
		else
			results = "Parameters are missing";

		return Content(results);
	}
}

When passing the string to the method, use the command name followed by any arguments.

Example:

using ReddCoinNet;
private string DoCommand(string input)
{
	Load.ConfigLocation = <Fully Qualified Path to Config File>;
	{
		if (Load.FileData())
		{
			string cmd = string.Empty;
			string[] line_args = new string[1];
			data = id;
			if (data != null)
			{
				line_results = data.Split(' ');
				if (line_results.Length > 0)
				{
					cmd = line_results[0];
					line_args = new string[line_results.Length - 1];
					if (line_results.Length == 1)
					{
						line_args = null;
					}
					else
					{
						for (int x = 0; x < line_args.Length; x++)
						{
							line_args[x] = line_results[x + 1];
						}
					}
					results = Parse.Parse_cmd(cmd, line_args);
				}
				else
				{
				}
			}
			else
				results = "Parameters are missing";
		}
		else
			results = "Parameters are missing";

		return results;
	}
}
private string MakeCommand()
{
	//Use Try/Catch/Finally loops for more robust programming...
	
	string result = string.Empty;
	string addresses = string.Empty;
	address = RdXd6m9nZ6GsUA6ZXLJjiyuKeS3vvsS7NX,171sgjn4YtPu27adkKGrdDwzRTxnRkBfKV;
	
	//results in a new reddcoin address with no account name
	result = DoCommand("2 addresses);
	
	//results in a new reddcoin address with account name SuperAwesome
	result = DoCommand("2 addresses SuperAwesome);
	
	return result;
}

ReddCoin Donations: Rc1MZY3Wh8GFoyXiCNXjTnTTS2xsYNJUQx
codereddgames@gmail.com


