Thanks to Sir Owain Kenway for this [video](https://www.youtube.com/watch?v=w8xCLxd7H0o) and the associated [github repo](https://github.com/owainkenwayucl/Garbage/tree/master/snippets/Matlab-Jupyter).

My implementation (simpler requirements):

1. Create a venv on stroom with the following requirements.txt

```python
jupyterlab 
jupyter-matlab-proxy
notebook<7.0.0
```
NB: use notebook ver < 7.0.0

2. Mount the venv and launch the jupyter lab server, e.g.

```bash
jupyter lab --no-browser --port=5100
```

3. Connect to stroom with VS code and open the corresponding port.

4. Enjoy `localhost:5100` in your local browser (you might need to cp/paste the full address with the token)



 
