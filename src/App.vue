<template>
  <div class="container">
    <h1 class="title">HTML To Markdown Previewer</h1>
    <div v-if="!oExpanded" class="inputBox collapsed">
      <div class="header">
        <i class="fa fa-free-code-camp" aria-hidden="true"></i>
        <h3>Editor</h3>
        <a href="#" id="Edit" @click="expand">
          <i v-if="!iExpanded" class="fa fa-arrows-alt" aria-hidden="true"></i>
          <i v-else class="fa fa-compress" aria-hidden="true"></i>
        </a>
      </div>
      <textarea class="input" v-model="input"></textarea>
    </div>
    <div v-if="!iExpanded" class="outputBox">
      <div class="header">
        <i class="fa fa-free-code-camp" aria-hidden="true"></i>
        <h3>Previewer</h3>
        <a href="#" id="Preview" @click="expand">
          <i v-if="!oExpanded" class="fa fa-arrows-alt" aria-hidden="true"></i>
          <i v-else class="fa fa-compress" aria-hidden="true"></i>
        </a>
      </div>
      <div class="output" v-html="toMarkdown"></div>
    </div>
  </div>
</template>

<script>
import {marked} from 'marked';

export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      iExpanded: false,
      oExpanded: false,
      input: `## Below is text from my input converted to markdown using marked.js
------------------
### This was pretty simple to set up

Heres some code, \`<div></div>\`, between 2 backticks.

\`\`\`
// this is multi-line code:

function anotherExample(firstLine, lastLine) {
  if (firstLine == '\`\`\`' && lastLine == '\`\`\`') {
    return multiLineCode;
  }
}
\`\`\`
There's also [links](https://www.freecodecamp.org), and
> Block Quotes!
`,
    }
  },
  computed: {
    toMarkdown() {
      return marked(this.input);
    },
  },
  methods: {
    expand(item) {
      let name = item.target.parentElement.id;
      
      if (name == 'Edit') {
        this.iExpanded = !this.iExpanded;
        let ele = document.querySelector('.inputBox');
        if (this.iExpanded) {
          ele.classList.remove('collapsed');
          ele.classList.add('expanded');
        } else {
          ele.classList.remove('expanded');
          ele.classList.add('collapsed');
        }
      // Converted Markdown
      } else if (name == 'Preview') {
        this.oExpanded = !this.oExpanded;
        let ele = document.querySelector('.outputBox');
        if (this.oExpanded) {
          ele.classList.add('expanded');
        } else {
          ele.classList.remove('expanded')
        }
      }
    }
  }
}
</script>
