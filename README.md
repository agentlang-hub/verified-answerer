# Example app: verified-answerer

This app comes up with an answer to a general question, and then
verifies the answer with a verifier agent. Finally, it provides the
answer along with the verification result.

## Usage

You need a Unix-compatible (macOS, Linux or Windows [WSL](https://learn.microsoft.com/en-us/windows/wsl/install))
system to run this app. Open a terminal and execute the steps below:

To run this app you need to define these env vars:

```shell
export OPENAI_API_KEY="FIXME" # your OpenAI API key
```

You may run this app without making a local copy first (i.e. clone the repo)
using Docker as follows:

```shell
docker run --rm \
  -p "0.0.0.0:8080:8080" \
  -v $PWD:/agentlang \
  -e OPENAI_API_KEY="$OPENAI_API_KEY" \
  -it agentlang/agentlang.cli:latest \
  agent clonerun https://github.com/agentlang-hub/verified-answerer.git
```

### Running a local copy of the app

If you have cloned the app and made a local copy on your computer,
you may run it using Docker as follows:

```shell
docker run --rm \
  -p "0.0.0.0:8080:8080" \
  -v $PWD:/agentlang \
  -e OPENAI_API_KEY="$OPENAI_API_KEY" \
  -it agentlang/agentlang.cli:latest \
  agent run
```

Alternatively, instead of Docker you may use the locally installed
[Agentlang CLI](https://github.com/agentlang-ai/agentlang.cli):

```shell
agent run
```

### Getting the app to provide verified answers

Make a request to ask a question as follows:

```shell
curl -X POST \
  localhost:8080/api/VerifiedAnswerer.Core/AnswerWithVerification \
  -H 'Content-type: application/json' \
  -d '{"VerifiedAnswerer.Core/AnswerWithVerification": {"UserInstruction": "Who was the least decorated (minimum medals) individual athlete in the Olympic games that were held at Sydney?"}}'
```

It should respond with a JSON response body, example below:

```json
[
  {
    "status": "ok",
    "result": [
      "Leisel Jones is an Australian former competitive swimmer who is one of the most successful breaststroke swimmers in history. She has won a total of nine Olympic medals, including three gold medals, and has set multiple world records in her career.\n\nOne of the key factors contributing to Leisel Jones' success in breaststroke swimming is her technique. Jones was known for her efficient and powerful breaststroke technique, which allowed her to maintain a strong and consistent stroke throughout her races. Her ability to execute the technical aspects of the breaststroke effectively played a significant role in her success in the pool.\n\nIn addition to her technical proficiency, Leisel Jones also had a strong mental game that helped her perform at the highest level. She was known for her focus, determination, and competitive spirit, which enabled her to excel in high-pressure situations such as Olympic competitions. Jones' mental toughness and ability to stay composed under pressure were key factors in her success as a breaststroke swimmer.\n\nANSWER: Leisel Jones' success as a breaststroke swimmer can be attributed to her efficient and powerful technique, as well as her strong mental game and competitive spirit.",
      "The user asked \"Is the conclusion correct?\" and the other agent replied \"YES\"."
    ],
    "message": null
  }
]
```

## License

Copyright 2024-2025 Fractl Inc.

Licensed under the Apache License, Version 2.0:
http://www.apache.org/licenses/LICENSE-2.0

