VERCEL_TOKEN= m5KGRpYlkExcVaOoNcxcwPxT
working fine frontend
===
{
  "version": 2,
  "name": "my-bitcoin-project",
  "builds": [
    { "src": "app.py", "use": "@vercel/python" },
    { "src": "templates/index.html", "use": "@vercel/static" }
  ],
  "routes": [
    { "src": "/predict", "dest": "/app.py" }, 
    { "src": "/", "dest": "/templates/index.html" }
  ]
}