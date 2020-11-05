# Worth_Knowing_Note
Records for worth things you known.

## <Situation 1> Definitely installed modules in conda env, but I cannot import the installed module in jupyter(lab or notebook).
- So, I shown up the path of those(__sys.path__), python in terminal & python in jupyter notebook(or lab).<br>
but although I executed the jupyter within conda env, its path didn't follow the env's path. (python in terminal in conda env has correct env path.)

- Through many googling and Q&A, I finally encountered someone's question in the similar situation like me.<br>
(-> https://stackoverflow.com/questions/46634660/jupyter-notebook-wrong-sys-path-and-sys-executable/46641050#46641050?newreg=3daad8577e9b476d80676a7a9b81b0c2)

- The questioner had solved by himself, and he said...<br>
  - I figured out the solution, since the kernel was set to use the default mac os x's python I fixed it by using the commands <br>
  python -m pip install ipykernel<br>
  python -m ipykernel install --user<br>
  (___All the command had been executed in working env.___)

- Thanks to his own solution, Finally my own Jupyter in conda env has been in correct env path.

## <Situation 2> In ssh server, I usally used jupyter(notebook or lab) remotely to be possible to work in local laptop. But the remotely access suddenly forbidden.
- __The strategy what I usually did to do it.__<br>
  - [zoshs2@ssh ~]$ jupyter notebook --no-browser --port=#### 
  - [zoshs2@local ~]$ ssh -NfL localhost:%%%%:localhost:#### zoshs2@ssh.server.address_or_ip
  - __Then, this message happened and the access has forbidden.__<br>
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@<br>
  @    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @<br>
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@<br>
  IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!<br>
  Someone could be eavesdropping on you right now (man-in-the-middle attack)!<br>
  It is also possible that a host key has just been changed.<br>
  The fingerprint for the ED25519 key sent by the remote host is<br>
  SHA256:FOJNTXkWRPYNC3Gk20Pqv8VsueOfZEbBVJO0QFUCP60.<br>
  Please contact your system administrator.<br>
  Add correct host key in /Users/yungi/.ssh/known_hosts to get rid of this message.<br>
  Offending ED25519 key in /Users/yungi/.ssh/known_hosts:1<br>
  ED25519 host key for gate.sscc.uos.ac.kr has changed and you have requested strict checking.<br>
  Host key verification failed.<br>
- Its solution can get from this blog.<br>
(-> https://cpuu.postype.com/post/30065)
- This warning is called __"Man in the middle attack(중간자 공격)"__.<br>
즉, IP(or address)로 기존에 접속한 적이 있는 서버와 RSA 공유키를 교환해오던 상태에서, 어느 날 서버가 알고있던 정보를 찾아서 따라갔더니 기존의 있던 서버와 '달라졌다'는 것이다.<br>
- To solve this problem, we should __initialize__ the linking keygen by commands.<br>
  - [zoshs2@local ~]$ ssh-keygen -R [IP or DomainAddress]<br>
    ex) $ ssh-keygen -R gate.sscc.uos.ac.kr (_I used its __DomainAddress___)<br>
  - Then, re-try to access the ssh(remote) server. __Done!!__
  
    
