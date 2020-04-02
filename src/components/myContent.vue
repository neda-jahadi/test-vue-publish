<template>
    <div class="component">
        <div class="tabs">
            <div class="titles">
                {{selectedTab}}
                <button
                    :class="counterSelectedClass"
                    @click="selectedTab = 'counter'">Counter</button>
                    
                <button
                    :class="counter2SelectedClass"
                    @click="selectedTab = 'counter2'">Counter</button>
                    
                <button
                    :class="authSelectedClass"
                    @click="selectedTab = 'authentication'">Authentication</button>
                    
            </div>
            <div class="content">

                <!-- Making a separate Counter component simplifies the template and Vue object in this component. -->
                <!-- You can test the difference between v-if and v-show by running the app, clicking the counter buttons, change tab and change back. The tab using v-if "forgets" the value. That is because v-if removes the element from the DOM if the condition is false. If this line is too long to read, you really should enable WORD WRAP globally in your editor. Check the slides for first Vue lesson. -->
                <Counter v-if="selectedTab == 'counter'" />

                <Counter v-show="selectedTab == 'counter2'" />

                <div v-show="selectedTab == 'authentication'">
                    <!-- You can debug your app by printing the value of data props and computed properties. -->
                     {{ isAuthenticated }} 
                    <button v-if="isAuthenticated"
                    @click="$emit('signOut')">Sign out</button>
                    <button v-else
                    @click="$emit('signIn')">Sign in</button>
                    <!-- Using v-else guarantees that one button is always visible. -->
                </div>
            </div>
        </div>
        <!-- Uh-oh, callback hell! Try to avoid this in your files, by moving code into components. -->
    </div>
</template>

<script>
import Counter from './Counter'

export default {
    name: '',
    props: {
        // isAuthenticated comes from the parent, App component. Do not change the value of it directly, instead $emit an event and let the parent change the value.
        isAuthenticated: Boolean(false)
    },
    data: () => ({
        selectedTab: 'counter'
    }),
    computed: {
        // Later in the course, we will see a better way to implement a tabbed component, using a list.
        counterSelectedClass() {
            // This code can be simplified using the conditional (ternary) expression
            if( this.selectedTab == 'counter' )
                return 'selected';
            return '';
        },
        counter2SelectedClass() {
            if( this.selectedTab == 'counter2' )
                return 'selected';
            return '';
        },
        authSelectedClass() {
            if( this.selectedTab == 'authentication' )
                return 'selected';
            return '';
        }
    },
    components: { Counter }
}
</script>

<style scoped>
.component {
    padding: 1em;
}
.component > div {
    /* background-color: red; */
    margin-bottom: 1em;
}
.component > div:last-child {
    margin-bottom: 0px;
}

.tabs > .titles {
    display: flex;
}
.tabs > .titles > button {
    margin-right: 2px;
    border: 1px solid black;
    background-color: lightgray;
}
.tabs > .content {
    background-color: lightgray;
    padding: 1em;
}
/* !important är FEL, gör selektorn mer specifik i stället */
.tabs button.selected {
    background-color: tomato;
}
</style>