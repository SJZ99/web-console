<template>
  <div id="background-terminal">
    <div id="wrapper">
      <vue-terminal
        title="console"
        defaultTaskCommandd="init console"
        :task-list="taskList"
        :command-list="commandList"
        :showHeader=false
        :unknownCommandMessage=unknownCommandMessage
        :autoFucos=true
      />
    </div>
  </div>
</template>

<script>
  import VueTerminal from 'vue-terminal';
  let helloBanner = `
,--.  ,--.  ,--. 
|  '--'  |  |  | 
|  .--.  |  |  | 
|  |  |  |  |  | 
\`--'  \`--ˊ  \`--ˊ 
`;
  
  export default {
    components: { VueTerminal },
    data: () => ({
      unknownCommandMessage: {
        time: "",
        type: 'error',
        label: 'Error',
        message: "This command haven't been developed!"
      },

      commandList: {
        hello: {
          description: "say hi",
          messages: [
            {
              message: helloBanner,
            }
          ]
        },
        version: {
          description: "show version info",
          messages: [
            {
              message: ".2.0 - August 4th only",
            }
          ]
        },
        findBrain: {
          description: "find out where your brain is.",
          messages: [
            {
              type: "error",
              label: "Error",
              message: "Missing! Couldn't find your brain:)"
            }
          ]
        }
      },

      taskList: {
        cowsay: {
          description: "let cow say something:))\n\t\t\t e.g., cowsay hello",
          cowsay(pushToList, input) {
            if(input.length <= 7) {
              input = "cowsay What else can I say?"
            }
            let talk = input.substr(6, input.length - 1);
            let upper = "_";
            let lower = "-";
            let length = input.length - 5;
            for(let i = 0; i < length; ++i) {
              upper = upper.concat("_");
              lower = lower.concat("-")
            }
            const p = new Promise(resolve => {
              pushToList({ time: "", label: 'Cow Say', type: 'success', message: `
      ${upper}
      <${talk} >
      ${lower}
      \\
       \\    ^__^
        \\   (oo)\\_______
            (__)\\       )\\/\\
                ||----w |
                ||     ||
              ` });
              resolve({ type: 'success', label: '', message: '' })
            })
            return p
          }
        }
      },
      
    }),
    computed: {
      
    }
  }
</script>

<style scoped>
#background-terminal {
  background: #010924;
  width: 100vw;
  height: 100vh;
  margin: 0px;
}

.vue-terminal {
  margin-bottom: 0px !important;
}
</style>
