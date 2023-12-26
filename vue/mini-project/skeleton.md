#### Skeleton Using Suspense

```vue

    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

    <div id="app">

        <suspense>
            <template #default>
                <async-component></async-component>
            </template>
            <template #fallback>
                Loading...
            </template>
        </suspense>
    </div>

    <script>
        const {
            createApp,
            defineAsyncComponent
        } = Vue

        const AsyncComponent = defineAsyncComponent(async () => {
            // Simulating a longer asynchronous operation
            await new Promise((resolve) => setTimeout(resolve, 5000));
            return {
                template: `<div>{{ data }}</div>`,
                data() {
                    return {
                        data: "Hi"
                    };
                }
            };
        });

        createApp({
            data() {
                return {
                    message: 'Hello Vue!',
                    data: "",
                }
            },
            async created() {
                await this.hello();
            },
            methods: {
                async hello() {
                    await new Promise((resolve) => {
                        setTimeout(() => {
                            this.data = "Hi";
                            resolve("Manage");
                        }, 4000);
                    });
                }
            },
        }).component('AsyncComponent', AsyncComponent).mount('#app')
    </script>

```
