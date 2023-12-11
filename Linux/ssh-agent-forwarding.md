# SSH agent forwarding
- Enables forwarding of the authentication agent connection
- Using local private key for login remote systems behind bastion.
- Avoid Coping private key to the bastion.

## By Command 
```
ssh -A user@bastion.com // -A option enables forwarding of the authentication agent connection.
```

## By Configuration
```
vim ~/.ssh/config
Host bastion.com
  ForwardAgent yes
```

## References
- https://dev.to/levivm/how-to-use-ssh-and-ssh-agent-forwarding-more-secure-ssh-2c32
