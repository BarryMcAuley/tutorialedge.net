<template>
    <div class="snippet">
        <Loading v-if="this.loading" />
        
        <div class="snippet-editor">
            <div class="window-header">
                <div class="action-buttons"></div>
                <span class="language">{{ this.language }}</span>
            </div>
            <codemirror v-model="code" :options="cmOptions" />
        </div>

        <div class="controls">
            <button v-on:click="executeCode" class="btn btn-primary btn-execute">Submit Code</button>
            <div class="output-label">
                <h5>Progam Output:</h5>
                <p>{{ this.output.time }}</p>
            </div>
            <pre class="output">{{ this.output.output }}</pre>
        </div>

        <hr>

        <Carbon />
    </div>
</template>

<script>
import { codemirror } from 'vue-codemirror';
import Carbon from '../misc/Carbon.vue';
import axios from 'axios';
import config from 'environment';
import Loading from '../misc/Loading.vue';

export default {
    name: 'Snippet',
    props: [
        "code",
        "language"
    ],
    components: {
        codemirror,
        Carbon,
        Loading
    },
    data () {
        return {
            code: "",
            output: "",
            loading: false,
            cmOptions: {
                tabSize: 4,
                mode: 'text/x-' + this.language,
                theme: 'monokai',
                lineNumbers: true,
                line: true,
            },
            terminalOptions: {
                tabSize: 4,
                theme: 'monokai',
                mode: 'application/html',
                lineNumbers: false,
                readOnly: true,
                cursorBlinkRate: -1,
                lineWrapping: true
            }
        }
    },
    methods: {
        executeCode: async function() {
            this.loading = true;
            try {
                let req = {
                    code: this.code
                }

                let response = await axios({ method: "post", 
                    // url: config.apiBase + "/v1/execute" + this.language, 
                    url: config.goApiUrl + "/execute", 
                    data: JSON.stringify(req),
                    headers: {
                        "Authorization": "Bearer " + this.$auth.getAccessToken(),
                        "Content-Type": "application/json"
                    }
                });
                this.loading = false;
                this.output = response.data;
            } catch (err) {
                this.loading = false;
                this.output = err;
            }
        }
    }
}
</script>

<style lang="scss">
.output-label {
    display: flex;
    -webkit-box-pack: justify;
    justify-content: space-between;
    font-family: monospace;
}

</style>