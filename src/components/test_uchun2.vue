<template>
    <div class="app">
        <h2>Language Translation</h2>
        <div class="dropdown">
            <button class="btn btn-outline-secondary dropdown-toggle" type="button" id="lng-dropdown"
                data-bs-toggle="dropdown" aria-expanded="false">
                {{ langLabel }}
            </button>
            <ul class="dropdown-menu" aria-labelledby="lng-dropdown">
                <li><a class="dropdown-item" @click="handlclick(0)">{{ options[0].label }}</a></li>
                <li><a class="dropdown-item" @click="handlclick(1)">{{ options[1].label }}</a></li>
                <li><a class="dropdown-item" @click="handlclick(2)">{{ options[2].label }}</a></li>
            </ul>
        </div>
        <div class="translation">
            <h3>{{ selectedLanguage }}</h3>
            <p>{{ translation }}</p>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            options: [
                { value: 'en', label: 'English' },
                { value: 'ru', label: 'Russian' },
                { value: 'uz', label: 'Uzbekistan' }
            ],
            selectedLanguage: 'Uzbekistan',
            translation: ''
        };
    },
    methods: {
        handlclick(index) {
            this.selectedLanguage = this.options[index].label;
            this.translateText(this.selectedLanguage);
        },
        translateText(language) {
            // Sizning til tarjima logikangizni shu yerdan yozing
            if (language === 'English') {
                this.translation = 'Hello! Welcome to the language translation app.';
            } else if (language === 'Russian') {
                this.translation = 'Привет! Добро пожаловать в приложение для перевода языков.';
            } else if (language === 'Uzbekistan') {
                this.translation = 'Salom! Til tarjima ilovaligiga hush kelibsiz.';
            }
        }
    },
    mounted() {
        this.translateText(this.selectedLanguage);
    }
};
</script>

<style>
.app {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 20px;
}

.dropdown {
    position: relative;
    display: inline-block;
}

.translation {
    margin-top: 20px;
    text-align: center;
}
</style>