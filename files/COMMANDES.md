# Workshop 2 – commandes à taper sur le PC du labo

```bash
# 0) vérifier le noyau (doit être < 6.19 ou > 7.0.13)
uname -r

# 1) JSON
nano movistar.json          # copier le contenu de files/movistar.json
python3 -m json.tool movistar.json   # ou jsonlint.com

# 2) YAML avec yq
sudo wget -qO /usr/bin/yq https://github.com/mikefarah/yq/releases/latest/download/yq_linux_amd64
sudo chmod a+x /usr/bin/yq
yq --version
yq -Poy movistar.json > movistar.yaml
cat movistar.yaml
yq -Poj movistar.yaml
yq -Poc movistar.json              # -> erreur "csv encoding only works for arrays"
yq -Poc '.users' movistar.json     # -> solution
yq -oy '.users[].idUE |= to_string' movistar.json   # idUE en string

# 3) MongoDB import
mongoimport --db users --collection movistar --file movistar.json
mongosh
#   use users
#   show collections
#   db.movistar.find()        <- faire la capture d'écran ici

# 4) MongoDB export
mongoexport --db users --collection movistar --out users.json
cat users.json
```

Attention : l'ObjectId (`_id`) et les heures seront différents sur ton PC.
Si tu refais l'import, mets à jour la section 4 du rapport (le décodage du timestamp).
