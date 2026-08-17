## CLAUDE.md
Ich habe alle Befehle (npm run dev, npm test, npm run lint) und die Architecture 
(server.js, routes/, db/store.js) reingeschrieben. 
Bewusst weggelassen: Code-Beispiele, weil die aus dem Code selbst ersichtlich sind.
Auch keine .env-Beispiele, weil die in .env.example schon existieren.
## Permissions
allow: Bash(npm test:*) - damit Claude Tests ausführen kann, ohne nachzufragen
ask: Bash(git push:*) - will ich jedes Mal bestätigen
deny: Read(./.env) - würde sonst Secrets preisgeben
deny: Bash(git push --force:*) - würde den Git-Verlauf zerstören
