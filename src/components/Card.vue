<template>
    <div class="card">
        <button @click="changeColors" class="color-change-btn" :style="{ backgroundColor: cardBackgroundColor }">Trocar
            cor</button>
        <div class="card-container">
            <div class="card-img" :style="{ backgroundColor: cardBackgroundColor }">
                <div v-if="user && user.image">
                    <img :src="getUserImageUrl()" alt="User Image" :style="{ border: imageBorder }">
                </div>
            </div>
            <div class="card-info">
                <div v-if="user && (user.nome || user.sobrenome)">
                    <p>{{ user.nome }} <span class="sobrenome" :style="{ color: sobrenomeColor }">{{ user.sobrenome
                    }}</span>
                    </p>
                </div>
            </div>
        </div>

    </div>
</template>
  
<style scoped>
.card {
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 10px;
}

.card-container {
    border: 1px solid #cccccc;
    box-shadow: 10px 10px 15px -7px rgba(0,0,0,0.38);
}

.color-change-btn {
    border: none;
    padding: 10px;
    transition: 0.3s ease-in-out;
    color: #fff;
    border-radius: 5px;
}

.color-change-btn:hover {
    cursor: pointer;
}

.card-img {
    height: 150px;
    min-width: 100px;
    padding: 20px;
    transition: 0.3s ease-in-out;
}

.card-img img {
    width: 100%;
    max-height: 150px;
    object-fit: cover;
    transition: 0.3s ease-in-out;
}

.card-info {
    padding: 10px 20px;
    background-color: #000;
    color: #fff;
    border-top: 2px solid #cccccc;
    text-transform: capitalize;
    min-width: 120px;
}

.sobrenome {
    transition: 0.3s ease-in-out;
}
</style>

<script>
export default {
    data() {
        return {
            cardBackgroundColor: '#ECB117',
            sobrenomeColor: '#ECB117',
            imageBorder: '2px solid #000',
            colorToggle: false
        }
    },
    props: {
        user: {
            type: Object,
            required: true
        }
    },
    methods: {
        getUserImageUrl() {
            if (this.user.image) {
                return URL.createObjectURL(this.user.image);
            } else {
                return '';
            }
        },
        changeColors() {
            this.cardBackgroundColor = this.colorToggle ? '#ECB117' : '#9B0021'
            this.sobrenomeColor = this.colorToggle ? '#ECB117' : '#9B0021'
            this.imageBorder = this.colorToggle ? '2px solid #000' : '2px solid #fff'
            this.colorToggle = !this.colorToggle;
        }
    }
};
</script>
  