- Users may want to schedule a certain action or task to take place after the system has booted. Take, for example, backing up files. We're going to be talking about the `cron` process, but more specifically, how we can interact with it via the use of `crontabs`.

## Crontabs
- Crontab is one of the processes that is started during boot, which is responsible for facilitating and managing cron jobs.
- A crontab is simply a special file with formatting that is recognised by the `cron` process. 

### Crontabs require 6 specific values:
![[crontab.png]]
- An interesting feature of crontabs is that these also support the wildcard or asterisk (`*`). If we do not wish to provide a value for that specific field, i.e. we don't care what month, day, or year it is executed -- only that it is executed every 12 hours, we simply just place an asterisk.
- **This help you generate formatting for crontabs** - [crontab Generator](https://crontab-generator.org/)
- **Crontabs can be edited using** - 
```bash
crontab -e
```
