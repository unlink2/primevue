<template>
    <AppDoc name="StepsDemo" :sources="sources" :extPages="pages" github="steps/StepsDemo.vue">
        <h5>Import via Module</h5>
        <pre v-code.script><code>
import Steps from 'primevue/steps';

</code></pre>

        <h5>Import via CDN</h5>
        <pre v-code><code>
&lt;script src="https://unpkg.com/primevue@^3/core/core.min.js"&gt;&lt;/script&gt;
&lt;script src="https://unpkg.com/primevue@^3/steps/steps.min.js"&gt;&lt;/script&gt;

</code></pre>

        <h5>MenuModel</h5>
        <p>Steps uses the common MenuModel API to define the items, visit <router-link to="/menumodel">MenuModel API</router-link> for details.</p>

        <h5>Getting Started</h5>
        <p>Steps is integrated with Vue Router and requires a collection of menuitems as its model.</p>
        <pre v-code><code>
&lt;Steps :model="items" /&gt;
&lt;router-view /&gt;

</code></pre>

        <pre v-code.script><code>
export default {
	data() {
		return {
			items: [{
                label: 'Personal',
                to: '/steps'
            },
            {
                label: 'Seat',
                to: '/steps/seat'
            },
            {
                label: 'Payment',
                to: '/steps/payment'
            },
            {
                label: 'Confirmation',
                to: '/steps/confirmation'
            }]
		}
	}
}

</code></pre>

        <h5>Interactive</h5>
        <p>Items are readonly by default, if you'd like to make them interactive then disable <i>readonly</i> property.</p>
        <pre v-code><code>
&lt;Steps :model="items" :readonly="false" /&gt;
&lt;router-view /&gt;

</code></pre>

        <h5>Templating</h5>
        <p>Steps offers content customization with the <i>item</i> template that receives the menuitem instance from the model as a parameter.</p>
        <pre v-code><code><template v-pre>
&lt;Steps :model="items"&gt;
    &lt;template #item="{item}"&gt;
        &lt;a :href="item.url"&gt;{{item.label}}&lt;/a&gt;
    &lt;/template&gt;
&lt;/Steps&gt;
</template>
</code></pre>

        <p><i>router-link</i> with route configuration can also be used within templating for further customization.</p>
        <pre v-code><code><template v-pre>
&lt;Steps :model="items"&gt;
    &lt;template #item="{item}"&gt;
        &lt;router-link :to="item.to" custom v-slot="{href, route, navigate, isActive, isExactActive}"&gt;
            &lt;a :href="href" @click="navigate" :class="{'active-link': isActive, 'active-link-exact": isExactActive}&gt;{{route.fullPath}}&lt;/a&gt;
        &lt;/router-link&gt;
    &lt;/template&gt;
&lt;/Steps&gt;
</template>
</code></pre>

        <h5>Properties</h5>
        <p>Any property as style and class are passed to the main container element. Following are the additional properties to configure the component.</p>
        <div class="doc-tablewrapper">
            <table class="doc-table">
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Type</th>
                        <th>Default</th>
                        <th>Description</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>id</td>
                        <td>string</td>
                        <td>null</td>
                        <td>Unique identifier of the element.</td>
                    </tr>
                    <tr>
                        <td>model</td>
                        <td>array</td>
                        <td>null</td>
                        <td>An array of menuitems.</td>
                    </tr>
                    <tr>
                        <td>readonly</td>
                        <td>boolean</td>
                        <td>true</td>
                        <td>Whether the items are clickable or not.</td>
                    </tr>
                    <tr>
                        <td>exact</td>
                        <td>boolean</td>
                        <td>true</td>
                        <td>Whether to apply 'router-link-active-exact' class if route exactly matches the item path.</td>
                    </tr>
                </tbody>
            </table>
        </div>

        <h5>Slots</h5>
        <div class="doc-tablewrapper">
            <table class="doc-table">
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Parameters</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>item</td>
                        <td>item: Menuitem instance</td>
                    </tr>
                </tbody>
            </table>
        </div>

        <h5>Styling</h5>
        <p>Following is the list of structural style classes, for theming classes visit <router-link to="/theming">theming</router-link> page.</p>
        <div class="doc-tablewrapper">
            <table class="doc-table">
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Element</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>p-steps</td>
                        <td>Container element.</td>
                    </tr>
                    <tr>
                        <td>p-steps-item</td>
                        <td>Menuitem element.</td>
                    </tr>
                    <tr>
                        <td>p-steps-number</td>
                        <td>Number of menuitem.</td>
                    </tr>
                    <tr>
                        <td>p-steps-title</td>
                        <td>Label of menuitem.</td>
                    </tr>
                </tbody>
            </table>
        </div>

        <h5>Dependencies</h5>
        <p>None.</p>
    </AppDoc>
</template>

<script>
export default {
    data() {
        return {
            sources: {
                'options-api': {
                    tabName: 'Options API Source',
                    content: `
<template>
    <div>
        <Toast />
        
        <div class="card">
            <Steps :model="items" :readonly="true" />
        </div>

        <router-view v-slot="{Component}" :formData="formObject" @prevPage="prevPage($event)" @nextPage="nextPage($event)" @complete="complete">
            <keep-alive>
                <component :is="Component" />
            </keep-alive>
        </router-view>
    </div>
</template>

<script>
export default {
    data() {
        return {
            items: [{
                label: 'Personal',
                to: '/'
            },
            {
                label: 'Seat',
                to: '/seat'
            },
            {
                label: 'Payment',
                to: '/payment'
            },
            {
                label: 'Confirmation',
                to: '/confirmation'
            }],
            formObject: {}
        }
    },
    methods: {
        nextPage(event) {
            for (let field in event.formData) {
                this.formObject[field] = event.formData[field];
            }

            this.$router.push(this.items[event.pageIndex + 1].to);
        },
        prevPage(event) {
            this.$router.push(this.items[event.pageIndex - 1].to);
        },
        complete() {
            this.$toast.add({severity:'success', summary:'Order submitted', detail: 'Dear, ' + this.formObject.firstname + ' ' + this.formObject.lastname + ' your order completed.'});
        }
    }
}
<\\/script>

<style scoped lang="scss">
::v-deep(b) {
    display: block;
}

::v-deep(.p-card-body) {
    padding: 2rem;
}
</style>
                    `
                },
                'composition-api': {
                    tabName: 'Composition API Source',
                    content: `<template>
    <div>
        <Toast />

        <div class="card">
            <Steps :model="items" :readonly="true" />
        </div>

        <router-view v-slot="{Component}" :formData="formObject" @prevPage="prevPage($event)" @nextPage="nextPage($event)" @complete="complete">
            <keep-alive>
                <component :is="Component" />
            </keep-alive>
        </router-view>
    </div>
</template>

<script>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import { useToast } from 'primevue/usetoast';

export default {
    setup() {
        const router = useRouter();
        const toast = useToast();
        const items = ref([
            {
                label: 'Personal',
                to: "/"
            },
            {
                label: 'Seat',
                to: "/seat",
            },
            {
                label: 'Payment',
                to: "/payment",
            },
            {
                label: 'Confirmation',
                to: "/confirmation",
            }
        ]);
        const formObject = ref({});

        const nextPage = (event) => {
            for (let field in event.formData) {
                formObject.value[field] = event.formData[field];
            }

            router.push(items.value[event.pageIndex + 1].to);
        };
        const prevPage = (event) => {
            router.push(items.value[event.pageIndex - 1].to);
        };
        const complete = () => {
            toast.add({severity:'success', summary:'Order submitted', detail: 'Dear, ' + formObject.value.firstname + ' ' + formObject.value.lastname + ' your order completed.'});
        };

        return { items, formObject, nextPage, prevPage, complete }
    }
}
<\\/script>

<style scoped lang="scss">
::v-deep(b) {
    display: block;
}

::v-deep(.p-card-body) {
    padding: 2rem;
}
</style>
`
                },
                'browser-source': {
                    tabName: 'Browser Source',
                    imports: `<script src="https://unpkg.com/vue-router@4.0.0/dist/vue-router.global.js"><\\/script>
        <script src="https://unpkg.com/primevue@^3/steps/steps.min.js"><\\/script>
        <script src="https://unpkg.com/primevue@^3/toast/toast.min.js"><\\/script>
        <script src="https://unpkg.com/primevue@^3/toastservice/toastservice.min.js"><\\/script>
        <script src="https://unpkg.com/primevue@^3/card/card.min.js"><\\/script>
        <script src="https://unpkg.com/primevue@^3/inputnumber/inputnumber.min.js"><\\/script>
        <script src="https://unpkg.com/primevue@^3/inputmask/inputmask.min.js"><\\/script>
        <script src="https://unpkg.com/primevue@^3/checkbox/checkbox.min.js"><\\/script>`,
                    content: `<div id="app">
            <p-toast></p-toast>

            <div class="card">
                <p-steps :model="items" :readonly="true"></p-steps>
            </div>

            <router-view v-slot="{Component}" :form-data="formObject" @prev-page="prevPage($event)" @next-page="nextPage($event)" @complete="complete">
                <keep-alive>
                    <component :is="Component"></component>
                </keep-alive>
            </router-view>
        </div>

        <script type="module">
        const { createApp, ref } = Vue;
        const { useToast } = primevue.usetoast;

        const App = {
            setup() {
                const toast = useToast();
                const items = ref([
                    {
                        label: 'Personal',
                        to: "/"
                    },
                    {
                        label: 'Seat',
                        to: "/seat",
                    },
                    {
                        label: 'Payment',
                        to: "/payment",
                    },
                    {
                        label: 'Confirmation',
                        to: "/confirmation",
                    }
                ]);
                const formObject = ref({});

                const nextPage = (event) => {
                    for (let field in event.formData) {
                        formObject.value[field] = event.formData[field];
                    }

                    router.push(items.value[event.pageIndex + 1].to);
                };
                const prevPage = (event) => {
                    router.push(items.value[event.pageIndex - 1].to);
                };
                const complete = () => {
                    toast.add({severity:'success', summary:'Order submitted', detail: 'Dear, ' + formObject.value.firstname + ' ' + formObject.value.lastname + ' your order completed.'});
                };

                return { items, formObject, nextPage, prevPage, complete }
            },
            components: {
                "p-steps": primevue.steps,
                "p-toast": primevue.toast,
                "p-card": primevue.card
            }
        };

        const Personal = {
            template: \`<div class="stepsdemo-content">
                <p-card>
                    <template v-slot:title>
                        Personal Information
                    </template>
                    <template v-slot:subtitle>
                        Enter your personal information
                    </template>
                    <template v-slot:content>
                        <div class="p-fluid">
                            <div class="field">
                                <label for="firstname">Firstname</label>
                                <p-inputtext id="firstname" v-model="firstname" :class="{'p-invalid': validationErrors.firstname && submitted}"></p-inputtext>
                                <small v-show="validationErrors.firstname && submitted" class="p-error">Firstname is required.</small>
                            </div>
                            <div class="field">
                                <label for="lastname">Lastname</label>
                                <p-inputtext id="lastname" v-model="lastname" :class="{'p-invalid': validationErrors.lastname && submitted}"></p-inputtext>
                                <small v-show="validationErrors.lastname && submitted" class="p-error">Lastname is required.</small>
                            </div>
                            <div class="field">
                                <label for="age">Age</label>
                                <p-inputnumber id="age" v-model="age"></p-inputnumber>
                            </div>
                        </div>
                    </template>
                    <template v-slot:footer>
                        <div class="grid grid-nogutter justify-content-between">
                            <i></i>
                            <p-button label="Next" @click="nextPage()" icon="pi pi-angle-right" icon-pos="right"></p-button>
                        </div>
                    </template>
                </p-card>
            </div>\`,
            data () {
                return {
                    firstname: '',
                    lastname: '',
                    age: null,
                    submitted: false,
                    validationErrors: {}
                }
            },
            methods: {
                nextPage() {
                    this.submitted = true;
                    if (this.validateForm() ) {
                        this.$emit('next-page', {formData: {firstname: this.firstname, lastname: this.lastname, age: this.age}, pageIndex: 0});
                    }
                },
                validateForm() {
                    if (!this.firstname.trim())
                        this.validationErrors['firstname'] = true;
                    else
                        delete this.validationErrors['firstname'];

                    if (!this.lastname.trim())
                        this.validationErrors['lastname'] = true;
                    else
                        delete this.validationErrors['lastname'];

                    return !Object.keys(this.validationErrors).length;
                }
            },
            components: {
                "p-card": primevue.card,
                "p-inputtext": primevue.inputtext,
                "p-inputnumber": primevue.inputnumber,
                "p-button": primevue.button 
            }
        };

        const Seat = {
            template: \`<div class="stepsdemo-content">
                <p-card>
                <template v-slot:title>
                        Seat Information
                    </template>
                    <template v-slot:subtitle>
                        Choose your seat
                    </template>
                    <template v-slot:content>
                        <div class="p-fluid formgrid grid">
                            <div class="field col-12 md:col-6">
                                <label for="class">Class</label>
                                <p-dropdown input-id="class" v-model="selectedClass" :options="classes" @change="setWagons($event)" option-label="name" placeholder="Select a Class"></p-dropdown>
                            </div>
                            <div class="field col-12 md:col-6">
                                <label for="lastname">Wagon</label>
                                <p-dropdown input-id="wagon" v-model="selectedWagon" :options="wagons" @change="setSeats($event)" option-label="wagon" placeholder="Select a Wagon"></p-dropdown>
                            </div>
                            <div class="field col-12">
                                <label for="seat">Seat</label>
                                <p-dropdown input-id="seat" v-model="selectedSeat" :options="seats" option-label="seat" placeholder="Select a Seat"></p-dropdown>
                            </div>
                        </div>
                    </template>
                    <template v-slot:footer>
                        <div class="grid grid-nogutter justify-content-between">
                            <p-button label="Back" @click="prevPage()" icon="pi pi-angle-left"></p-button>
                            <p-button label="Next" @click="nextPage()" icon="pi pi-angle-right" icon-pos="right"></p-button>
                        </div>
                    </template>
                </p-card>
            </div>\`,
            data() {
                return {
                    selectedClass: '',
                    classes: [
                        {name: 'First Class', code: 'A', factor: 1},
                        {name: 'Second Class', code: 'B', factor: 2},
                        {name: 'Third Class', code: 'C', factor: 3}
                    ],
                    wagons: [],
                    selectedWagon: '',
                    seats: [],
                    selectedSeat: ''
                }
            },
            methods: {
                setWagons(event) {
                    if (this.selectedClass && event.value) {
                        this.wagons = [];
                        this.seats = [];
                        for (let i = 1; i < 3 * event.value.factor; i++) {
                            this.wagons.push({wagon: i + event.value.code, type: event.value.name, factor: event.value.factor});
                        }
                    }
                },
                setSeats(event) {
                    if (this.selectedWagon && event.value) {
                        this.seats = [];
                        for (let i = 1; i < 10 * event.value.factor; i++) {
                            this.seats.push({seat: i, type: event.value.type});
                        }
                    }
                },
                nextPage() {
                    this.$emit('next-page', {formData: {class: this.selectedClass.name, wagon: this.selectedWagon.wagon, seat: this.selectedSeat.seat}, pageIndex: 1});
                },
                prevPage() {
                    this.$emit('prev-page', {pageIndex: 1});
                }
            },
            components: {
                "p-card": primevue.card,
                "p-dropdown": primevue.dropdown,
                "p-button": primevue.button
            }
        };

        const Payment = {
            template: \`<div class="stepsdemo-content">
                <p-card>
                    <template v-slot:title>
                        Payment Information
                    </template>
                    <template v-slot:subtitle>
                        Enter your card details
                    </template>
                    <template v-slot:content>
                        <div class="p-fluid formgrid grid">
                            <div class="field col-12">
                                <label for="class">Card Holder Name</label>
                                <p-inputtext type="text" v-model="cardholderName"></p-inputext>
                            </div>
                            <div class="field col-8">
                                <label id="number" for="lastname">Number</label>
                                <p-inputmask id="number" mask="9999-9999-9999-9999" v-model="cardholderNumber"></p-inputmask>
                            </div>
                            <div class="field col-2">
                                <label id="date" for="date">Date</label>
                                <p-inputmask id="date" mask="99/99" v-model="date"></p-inputmask>
                            </div>
                            <div class="field col-2">
                                <label for="cvv">CVV</label>
                                <p-inputmask id="cvv" mask="999" v-model="cvv"></p-inputmask>
                            </div>
                            <div class="field-checkbox col-12">
                                <p-checkbox id="remember" v-model="remember" :binary="true"></p-checkbox>
                                <label for="remember" class="p-checkbox-label">Save credit card information for future</label>
                            </div>
                        </div>
                    </template>
                    <template v-slot:footer>
                        <div class="grid grid-nogutter justify-content-between">
                            <p-button label="Back" @click="prevPage()" icon="pi pi-angle-left"></p-button>
                            <p-button label="Next" @click="nextPage()" icon="pi pi-angle-right" icon-pos="right"></p-button>
                        </div>
                    </template>
                </p-card>
            </div>\`,
            data() {
                return {
                    cardholderName:'',
                    cardholderNumber:'',
                    date:'',
                    cvv:'',
                    remember:false
                }
            },
            methods: {
                nextPage() {
                    this.$emit('next-page', {formData: {cardholderName: this.cardholderName, cardholderNumber: this.cardholderNumber, date: this.date, cvv: this.cvv}, pageIndex: 2});
                },
                prevPage() {
                    this.$emit('prev-page', {pageIndex: 2});
                }
            },
            components: {
                "p-card": primevue.card,
                "p-inputtext": primevue.inputtext,
                "p-inputmask": primevue.inputmask,
                "p-checkbox": primevue.checkbox,
                "p-button": primevue.button
            }
        };

        const Confirmation = {
            template: \`<div class="stepsdemo-content">
                <p-card>
                    <template v-slot:title>
                        Confirmation
                    </template>
                    <template v-slot:content>
                        <div class="field col-12">
                            <label for="class">Name</label>
                            <b>{{formData.firstname ? formData.firstname : '-'}} {{formData.lastname ? formData.lastname : '-'}}</b>
                        </div>
                        <div class="field col-12">
                            <label for="Age">Age</label>
                            <b>{{formData.age ? formData.age : '-'}}</b>
                        </div>
                        <div class="field col-12">
                            <label for="Age">Seat Class</label>
                            <b>{{formData.class ? formData.class : '-'}}</b>
                        </div>
                        <div class="field col-12">
                            <label for="Age">Wagon Number</label>
                            <b>{{formData.vagon ? formData.vagon : '-'}}</b>
                        </div>
                        <div class="field col-12">
                            <label for="Age">Seat</label>
                            <b>{{formData.seat ? formData.seat : '-'}}</b>
                        </div>
                        <div class="field col-12">
                            <label for="Age">Cardholder Name</label>
                            <b>{{formData.cardholderName ? formData.cardholderName : '-'}}</b>
                        </div>
                        <div class="field col-12">
                            <label for="Age">Card Number</label>
                            <b>{{formData.cardholderNumber ? formData.cardholderNumber : '-'}}</b>
                        </div>
                        <div class="field col-12">
                            <label for="Age">Date</label>
                            <b>{{formData.date ? formData.date : '-'}}</b>
                        </div>
                        <div class="field col-12">
                            <label for="Age">CVV</label>
                            <b>{{formData.cvv && formData.cvv.length === 3  ? '**' + formData.cvv[2] : '-'}}</b>
                        </div>
                    </template>
                    <template v-slot:footer>
                        <div class="grid grid-nogutter justify-content-between">
                            <p-button label="Back" @click="prevPage()" icon="pi pi-angle-left"></p-button>
                            <p-button label="Complete" @click="complete()" icon="pi pi-check" icon-pos="right" class="p-button-success"></p-button>
                        </div>
                    </template>
                </p-card>
            </div>\`,
            props: {
                formData: Object
            },
            methods: {
                prevPage() {
                    this.$emit('prev-page', {pageIndex: 3});
                },
                complete() {
                    this.$emit('complete');
                }
            },
            components: {
                "p-card": primevue.card,
                "p-button": primevue.button
            }
        };

        const routes = [
            { path: "/", component: Personal },
            { path: "/seat", component: Seat },
            { path: "/payment", component: Payment },
            { path: "/confirmation", component: Confirmation }
        ];

        const router = VueRouter.createRouter({
            history: VueRouter.createWebHashHistory(),
            routes
        });

        createApp(App)
            .use(router)
            .use(primevue.config.default)
            .use(primevue.toastservice)
            .mount("#app");
        <\\/script>

        <style>
        b {
            display: block;
        }

        .p-card-body {
            padding: 2rem;
        }
        </style>
`
                }
            },
            pages: [
                {
                    tabName: 'PersonalDemo',
                    content: `
<template>
    <div class="stepsdemo-content">
        <Card>
            <template v-slot:title>
                Personal Information
            </template>
            <template v-slot:subtitle>
                Enter your personal information
            </template>
            <template v-slot:content>
                <div class="p-fluid">
                    <div class="field">
                        <label for="firstname">Firstname</label>
                        <InputText id="firstname" v-model="firstname" :class="{'p-invalid': validationErrors.firstname && submitted}" />
                        <small v-show="validationErrors.firstname && submitted" class="p-error">Firstname is required.</small>
                    </div>
                    <div class="field">
                        <label for="lastname">Lastname</label>
                        <InputText id="lastname" v-model="lastname" :class="{'p-invalid': validationErrors.lastname && submitted}" />
                        <small v-show="validationErrors.lastname && submitted" class="p-error">Lastname is required.</small>
                    </div>
                    <div class="field">
                        <label for="age">Age</label>
                        <InputNumber id="age" v-model="age" />
                    </div>
                </div>
            </template>
            <template v-slot:footer>
                <div class="grid grid-nogutter justify-content-between">
                    <i></i>
                    <Button label="Next" @click="nextPage()" icon="pi pi-angle-right" iconPos="right" />
                </div>
            </template>
        </Card>
    </div>
</template>

<script>
export default {
    data () {
        return {
            firstname: '',
            lastname: '',
            age: null,
            submitted: false,
            validationErrors: {}
        }
    },
    methods: {
        nextPage() {
            this.submitted = true;
            if (this.validateForm() ) {
                this.$emit('next-page', {formData: {firstname: this.firstname, lastname: this.lastname, age: this.age}, pageIndex: 0});
            }
        },
        validateForm() {
            if (!this.firstname.trim())
                this.validationErrors['firstname'] = true;
            else
                delete this.validationErrors['firstname'];

            if (!this.lastname.trim())
                this.validationErrors['lastname'] = true;
            else
                delete this.validationErrors['lastname'];

            return !Object.keys(this.validationErrors).length;
        }
    }
}
<\\/script>
`
                },
                {
                    tabName: 'SeatDemo',
                    content: `
<template>
    <div class="stepsdemo-content">
        <Card>
           <template v-slot:title>
                Seat Information
            </template>
            <template v-slot:subtitle>
                Choose your seat
            </template>
            <template v-slot:content>
                <div class="p-fluid formgrid grid">
                    <div class="field col-12 md:col-6">
                        <label for="class">Class</label>
                        <Dropdown inputId="class" v-model="selectedClass" :options="classes" @change="setVagons($event)" optionLabel="name" placeholder="Select a Class" />
                    </div>
                    <div class="field col-12 md:col-6">
                        <label for="lastname">Wagon</label>
                        <Dropdown inputId="wagon" v-model="selectedVagon" :options="vagons" @change="setSeats($event)" optionLabel="vagon" placeholder="Select a Vagon" />
                    </div>
                    <div class="field col-12">
                        <label for="seat">Seat</label>
                        <Dropdown inputId="seat" v-model="selectedSeat" :options="seats" optionLabel="seat" placeholder="Select a Seat" />
                    </div>
                </div>
            </template>
            <template v-slot:footer>
                <div class="grid grid-nogutter justify-content-between">
                    <Button label="Back" @click="prevPage()" icon="pi pi-angle-left" />
                    <Button label="Next" @click="nextPage()" icon="pi pi-angle-right" iconPos="right" />
                </div>
            </template>
        </Card>
    </div>
</template>

<script>
export default {
    data () {
        return {
            selectedClass: '',
            classes: [
                {name: 'First Class', code: 'A', factor: 1},
                {name: 'Second Class', code: 'B', factor: 2},
                {name: 'Third Class', code: 'C', factor: 3}
            ],
            vagons: [],
            selectedVagon: '',
            seats: [],
            selectedSeat: ''
        }
    },
    methods: {
        setVagons(event) {
            if (this.selectedClass && event.value) {
                this.vagons = [];
                this.seats = [];
                for (let i = 1; i < 3 * event.value.factor; i++) {
                    this.vagons.push({vagon: i + event.value.code, type: event.value.name, factor: event.value.factor});
                }
            }
        },
        setSeats(event) {
            if (this.selectedVagon && event.value) {
                this.seats = [];
                for (let i = 1; i < 10 * event.value.factor; i++) {
                    this.seats.push({seat: i, type: event.value.type});
                }
            }
        },
        nextPage() {
            this.$emit('next-page', {formData: {class: this.selectedClass.name, vagon: this.selectedVagon.vagon, seat: this.selectedSeat.seat}, pageIndex: 1});
        },
        prevPage() {
            this.$emit('prev-page', {pageIndex: 1});
        }
    }
}
<\\/script>
`
                },
                {
                    tabName: 'PaymentDemo',
                    content: `
<template>
    <div class="stepsdemo-content">
        <Card>
            <template v-slot:title>
                Payment Information
            </template>
            <template v-slot:subtitle>
                Enter your card details
            </template>
            <template v-slot:content>
                <div class="p-fluid formgrid grid">
                    <div class="field col-12">
                        <label for="class">Card Holder Name</label>
                        <InputText type="text" v-model="cardholderName" />
                    </div>
                    <div class="field col-8">
                        <label id="number" for="lastname">Number</label>
                        <InputMask id="number" mask="9999-9999-9999-9999" v-model="cardholderNumber" />
                    </div>
                    <div class="field col-2">
                        <label id="date" for="date">Date</label>
                        <InputMask id="date" mask="99/99" v-model="date" />
                    </div>
                    <div class="field col-2">
                        <label for="cvv">CVV</label>
                        <InputMask id="cvv" mask="999" v-model="cvv" />
                    </div>
                    <div class="field-checkbox col-12">
                        <Checkbox id="remember" v-model="remember" :binary="true" />
                        <label for="remember" class="p-checkbox-label">Save credit card information for future</label>
                    </div>
                </div>
            </template>
            <template v-slot:footer>
                <div class="grid grid-nogutter justify-content-between">
                    <Button label="Back" @click="prevPage()" icon="pi pi-angle-left" />
                    <Button label="Next" @click="nextPage()" icon="pi pi-angle-right" iconPos="right" />
                </div>
            </template>
        </Card>
    </div>
</template>

<script>
export default {
    data () {
        return {
            cardholderName:'',
            cardholderNumber:'',
            date:'',
            cvv:'',
            remember:false
        }
    },
    methods: {
        nextPage() {
            this.$emit('next-page', {formData: {cardholderName: this.cardholderName, cardholderNumber: this.cardholderNumber, date: this.date, cvv: this.cvv}, pageIndex: 2});
        },
        prevPage() {
            this.$emit('prev-page', {pageIndex: 2});
        }
    }
}
<\\/script>
`
                },
                {
                    tabName: 'ConfirmationDemo',
                    content: `
<template>
    <div class="stepsdemo-content">
        <Card>
            <template v-slot:title>
                Confirmation
            </template>
            <template v-slot:content>
                <div class="field col-12">
                    <label for="class">Name</label>
                    <b>{{formData.firstname ? formData.firstname : '-'}} {{formData.lastname ? formData.lastname : '-'}}</b>
                </div>
                <div class="field col-12">
                    <label for="Age">Age</label>
                    <b>{{formData.age ? formData.age : '-'}}</b>
                </div>
                <div class="field col-12">
                    <label for="Age">Seat Class</label>
                    <b>{{formData.class ? formData.class : '-'}}</b>
                </div>
                <div class="field col-12">
                    <label for="Age">Wagon Number</label>
                    <b>{{formData.vagon ? formData.vagon : '-'}}</b>
                </div>
                <div class="field col-12">
                    <label for="Age">Seat</label>
                    <b>{{formData.seat ? formData.seat : '-'}}</b>
                </div>
                <div class="field col-12">
                    <label for="Age">Cardholder Name</label>
                    <b>{{formData.cardholderName ? formData.cardholderName : '-'}}</b>
                </div>
                <div class="field col-12">
                    <label for="Age">Card Number</label>
                    <b>{{formData.cardholderNumber ? formData.cardholderNumber : '-'}}</b>
                </div>
                <div class="field col-12">
                    <label for="Age">Date</label>
                    <b>{{formData.date ? formData.date : '-'}}</b>
                </div>
                <div class="field col-12">
                    <label for="Age">CVV</label>
                    <b>{{formData.cvv && formData.cvv.length === 3  ? '**' + formData.cvv[2] : '-'}}</b>
                </div>
            </template>
            <template v-slot:footer>
                <div class="grid grid-nogutter justify-content-between">
                    <Button label="Back" @click="prevPage()" icon="pi pi-angle-left" />
                    <Button label="Complete" @click="complete()" icon="pi pi-check" iconPos="right" class="p-button-success"/>
                </div>
            </template>
        </Card>
    </div>
</template>

<script>
export default {
    props: {
        formData: Object
    },
    methods: {
        prevPage() {
            this.$emit('prev-page', {pageIndex: 3});
        },
        complete() {
            this.$emit('complete');
        }
    }
}
<\\/script>
`
                }
            ]
        };
    }
};
</script>
