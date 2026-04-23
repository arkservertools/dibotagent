# dibotagent
Discord Bot AI Agent.

# install
copy the docker compose file in one folder and run the stack.
```docker compose up -d```

# prepare ollama.
add the requiered llm models in ollama container (embeding model, and ai model)

```
docker exec -it ollama ollama pull nomic-embed-text
docker exec -it ollama ollama pull phi3.5
```

# Acces to the dibotagent web interface
https://localhost:8081
user admin
pwd admin123

# configure
configure it in web interface.
create your proyect, define the ai prompt, add your documents, create the bots.. etc.
check it calling the AI in web interface.
test it in your discord.

**more info in next days in this documents, please be patient.**



