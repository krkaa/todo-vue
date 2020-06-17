<template>
    <div id="app">
        <h1>TodoAPP for itprojects from Pavel Rusak</h1>
        <hr>

        <router-view />
    </div>
</template>

<style lang="scss">
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
        margin: 0 auto;
        width: 50%;
    }
    @media only screen and (max-width: 1200px) {
        #app {
            width: 60%
        }
    }
    @media only screen and (max-width: 992px) {
        #app {
            width: 70%
        }
    }
    @media only screen and (max-width: 768px) {
        #app {
            width: 80%
        }
    }
    @media only screen and (max-width: 600px) {
        #app {
            width: 100%
        }
    }

</style>
