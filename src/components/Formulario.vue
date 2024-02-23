<template>
    <div>
        <form class="form">
            <div class="form-image">
                <label>
                    <img v-if="user.image" :src="getUserImageUrl()" alt="Selected Image">
                    <span v-else>Selecionar Foto</span>
                </label>
                <input type="file" style="display: none;" ref="fileInput" @change="handleImageChange">
                <button @click.prevent="openFileInput">Adicionar Foto</button>
            </div>
            <div class="form-info">
                <div class="input">
                    <label for="nome">Nome</label>
                    <input type="text" id="nome" v-model="user.nome" @input="updateUser">
                </div>
                <div class="input">
                    <label for="sobrenome">Sobrenome</label>
                    <input type="text" id="sobrenome" v-model="user.sobrenome" @input="updateUser">
                </div>

            </div>

        </form>
    </div>
</template>

<style scoped>
.form {
    display: flex;
    align-items: start;
    border: 3px solid #cccccc;
    padding: 30px;
    gap: 10px;
}

.form-image {
    display: flex;
    flex-direction: column;
    gap: 10px;
    align-items: center;
}

.form-image label {
    border: 1px solid #000;
    width: 100%;
    height: 150px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.form-image label img {
    width: 100%;
    max-height: 150px;
    object-fit: cover;
}

.form-image label span {
    color: #cccccc;
}

.form-image button {
    border: none;
    color: #fff;
    background-color: #FF9900;
    padding: 10px;
    text-transform: uppercase;
}

.form-image button:hover {
    cursor: pointer;
}

.form-info {
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.form-info .input {
    display: flex;
    flex-direction: column;
}

.form-info .input label {
    font-size: 14px;
    margin-bottom: 5px;
}


.form-info .input input {
    width: 65%;
    border: 1px solid #cccccc;
    padding: 5px 10px;
    text-transform: uppercase;
}

@media(max-width: 468px) {
    .form {
        flex-direction: column;
        align-items: center;
        gap: 20px;
        padding: 20px 10px;
    }

    .form-image {
        max-width: 200px;
    }

    .form-info .input {
        width: 100%;
        align-items: center;
    }

    .form-info .input label {
        width: 145px;
    }

}
</style>
  
<script>
export default {
    data() {
        return {
            user: {
                nome: '',
                sobrenome: '',
                image: null
            }
        };
    },
    methods: {
        openFileInput() {
            this.$refs.fileInput.click();
        },
        handleImageChange(event) {
            const selectedFile = event.target.files[0];
            if (selectedFile) {
                this.user.image = selectedFile;
                this.updateUser();
            }
        },
        updateUser() {
            this.$emit('user-updated', this.user);
        },
        getUserImageUrl() {
            if (this.user.image) {
                return URL.createObjectURL(this.user.image);
            } else {
                return '';
            }
        }
    }
};
</script>
  