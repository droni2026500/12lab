<template>
        <div id="app">
            <h1>Записная книжка</h1>
            <div>
                <label>Фамилия:</label>
                <input type="text" placeholder="Антипов" v-model="params.secondName"/>
            </div> 
            <br>
            <div>
                <label>Имя:</label>
                <input type="text" placeholder="Андрей" v-model="params.firstName"/>
            </div>
            <br>
            <div>
                <label>Отчество:</label>
                <input type="text" placeholder="Витальевич" v-model="params.patronymic"/>
            </div> 
            <br>
            <div>
                <label>Телефонный номер:</label>
                <input type="text"  placeholder="+79258646122" v-model="params.phone"/>
            </div> 
            <br>
            <div>
                <label>Избранное:</label>
                <input type="checkbox" v-model="params.favorite"/>
            </div>
            <br>
            <div><label>Сортировка по:</label>
                Имени <input value="name1" type="radio" v-model="sort" v-on:click="onSort('name1')">
                Фамилии <input value="name2" type="radio" v-model="sort" v-on:click="onSort('name2')">
            </div>
            <br>
            <div>
                <button class="knopka" v-on:click="onAdd()">Добавить</button>
            </div>
            <div class="book">
                <li v-for="(item, index) in mas" v-bind:key=index>{{item.secondName}} {{item.firstName}} {{item.patronymic}} {{item.phone}}
                <span v-if="item.favorite"> ★ </span>
                </li>
            </div>
    </div>
</template>

<script>
export default {
        name: "notebook",
        data() {
            return {
                params: {
                firstName: "",
                secondName: "",
                patronymic: "",
                phone:"",
                favorite: false
            },
                sort: "name1",
                mas:[],
                flag: -1,
            }
        },
        methods: {

            onSort : function (param) {
                if(param === "name1") {
                    this.mas.sort((a, b) => a.firstName < b.firstName ? 1 : -1);
                }
                else if (param === "name2") {
                    this.mas.sort((a, b) => a.secondName < b.secondName ? 1 : -1);
                }
                this.mas.sort((a, b) => a.favorite < b.favorite ? 1 : -1);
            },

            onAdd: function () {
                    if (this.flag === -1) {
                        this.mas.push({
                            firstName: this.params.firstName,
                            secondName: this.params.secondName,
                            patronymic: this.params.patronymic,
                            phone: this.params.phone,
                            favorite: this.params.favorite
                        });
                    }
                    else {
                        this.mas[this.flag] = {
                            firstName: this.params.firstName,
                            secondName: this.params.secondName,
                            patronymic: this.params.patronymic,
                            phone: this.params.phone,
                            favorite: this.params.favorite
                        };
                            this.flag = -1;
                    }

                    if(this.sort === "name1") {

                        this.mas.sort((a, b) => a.firstName < b.firstName ? 1 : -1);
                    }
                    else if (this.sort === "name2") {

                        this.mas.sort((a, b) => a.secondName < b.secondName ? 1 : -1);
                    }

                    this.mas.sort((a, b) => a.favorite < b.favorite ? 1 : -1);

                    this.params.firstName = "";
                    this.params.secondName = "";
                    this.params.patronymic = "";
                    this.params.phone = "";
                    this.params.favorite = "";
            },
        }
}
</script>
