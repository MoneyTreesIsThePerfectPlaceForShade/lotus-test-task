<template>
    <div class="container">
        <header>
            <!-- Заголовок страницы -->
            <p class="header-trade">
                Ход торгов
                <strong
                    >Тестовые торги на ппарат ЛОТОС №2033564 (23.12.2022
                    08:00)</strong
                >
            </p>
            <hr />
            <p class="msg-for-traders">
                Уважаемые участники, во время вашего хода вы можете изменить
                параметры торгов, указанных в таблице:
            </p>
        </header>
        <article class="table-container">
            <!-- Блок с таблицей -->
            <!-- Скорее всего изначально стоило делать как таблицу -->
            <!-- Но ТЗ было в создании таймера, поэтому сделал через всё через css grid -->
            <p class="table-header">ХОД</p>
            <!-- Таймеры -->
            <p v-show="active120" class="timer-header timer-1">
                {{ displayMinutes1 }}:{{ displaySeconds1 }}
            </p>
            <p v-show="active240" class="timer-header timer-2">
                {{ displayMinutes2 }}:{{ displaySeconds2 }}
            </p>
            <p v-show="active360" class="timer-header timer-3">
                {{ displayMinutes3 }}:{{ displaySeconds3 }}
            </p>
            <p v-show="active480" class="timer-header timer-4">
                {{ displayMinutes4 }}:{{ displaySeconds4 }}
            </p>

            <p class="parametres">Параметры и требования</p>

            <p class="user-1">Участник №1</p>
            <p class="kompleks1">-</p>
            <p class="srok1">80</p>
            <p class="garant1">24</p>
            <p class="uslovia1">30%</p>
            <div class="stoimost1">
                <p class="blue">3,700,000 руб.</p>
                <p class="red">-25,000 руб.</p>
                <p class="green">2,475,000 руб.</p>
            </div>

            <p class="user-2">Участник №2</p>
            <p class="kompleks2">-</p>
            <p class="srok2">90</p>
            <p class="garant2">24</p>
            <p class="uslovia2">100%</p>
            <div class="stoimost2">
                <p class="blue">3,200,000 руб.</p>
                <p class="red">-25,000 руб.</p>
                <p class="green">2,475,000 руб.</p>
            </div>

            <p class="user-3">Участник №3</p>
            <p class="kompleks3">-</p>
            <p class="srok3">75</p>
            <p class="garant3">22</p>
            <p class="uslovia3">60%</p>
            <div class="stoimost3">
                <p class="blue">2,800,000 руб.</p>
                <p class="red">-25,000 руб.</p>
                <p class="green">2,475,000 руб.</p>
            </div>

            <p class="user-4">Участник №4</p>
            <p class="kompleks4">-</p>
            <p class="srok4">120</p>
            <p class="garant4">36</p>
            <p class="uslovia4">50%</p>
            <div class="stoimost4">
                <p class="blue">2,500,000 руб.</p>
                <p class="red">-25,000 руб.</p>
                <p class="green">2,475,000 руб.</p>
            </div>

            <p class="left-table1">
                Наличие комплекса мероприятий, повышающих стандарты качества
                изготовления
            </p>
            <p class="left-table2">Срок изготовления лота, дней</p>
            <p class="left-table3">Гарантийные обязательства, мес</p>
            <p class="left-table4">Условия оплаты</p>
            <p class="left-table5">
                Стоимость изготовления лота, руб (без НДС)
            </p>
            <p class="left-table6">Действия:</p>
        </article>
    </div>
</template>

<script>
export default {
    name: "TradeTable",
    data() {
        return {
            // вероятно, не самый эффективный способо, но ничего лучше я пока не придумал
            // для каждого участника сделал отдельный таймер, внизу значения в секундах
            timerCount1: 120,
            timerCount2: 240,
            timerCount3: 360,
            timerCount4: 480,
            // для красивого отображения
            displaySeconds1: "0" + 0,
            displayMinutes1: "0" + 2,
            displaySeconds2: "0" + 0,
            displayMinutes2: "0" + 2,
            displaySeconds3: "0" + 0,
            displayMinutes3: "0" + 2,
            displaySeconds4: "0" + 0,
            displayMinutes4: "0" + 2,
        };
    },

    computed: {
        // определяю значения секунд, минут и т.д. для дальнейшего использования
        _seconds: () => 1,
        _minutes() {
            return this._seconds * 60;
        },
        _hours() {
            return this._minutes * 60;
        },
        _days() {
            return this._hours * 24;
        },
        // эти computed переменные нужны для отображения таймера
        active120() {
            if (this.timerCount1 <= 0) {
                return false;
            } else if (this.timerCount1 > 0) {
                return true;
            } else return true;
        },
        active240() {
            if (this.timerCount2 >= 120 || this.timerCount2 <= 0) {
                return false;
            } else if (this.timerCount1 > 0) {
                return true;
            } else return true;
        },
        active360() {
            if (this.timerCount3 >= 120 || this.timerCount3 <= 0) {
                return false;
            } else if (this.timerCount1 > 0) {
                return true;
            } else return true;
        },
        active480() {
            if (this.timerCount4 >= 120 || this.timerCount4 <= 0) {
                return false;
            } else if (this.timerCount1 > 0) {
                return true;
            } else return true;
        },
    },
    watch: {
        // сами таймеры
        timerCount1: {
            handler(value) {
                if (value > 0) {
                    setTimeout(() => {
                        this.timerCount1--;
                        // для правильного отображения
                        const seconds = Math.floor(
                            (this.timerCount1 % this._minutes) / this._seconds
                        );
                        const minutes = Math.floor(
                            (this.timerCount1 % this._hours) / this._minutes
                        );

                        // для красивого отображения
                        this.displayMinutes1 =
                            minutes < 10 ? "0" + minutes : minutes;
                        this.displaySeconds1 =
                            seconds < 10 ? "0" + seconds : seconds;
                    }, 1000);
                }
            },
            immediate: true,
        },
        timerCount2: {
            handler(value) {
                if (value > 0) {
                    setTimeout(() => {
                        this.timerCount2--;
                        const seconds = Math.floor(
                            (this.timerCount2 % this._minutes) / this._seconds
                        );

                        const minutes = Math.floor(
                            (this.timerCount2 % this._hours) / this._minutes
                        );

                        this.displayMinutes2 =
                            minutes < 10 ? "0" + minutes : minutes;
                        this.displaySeconds2 =
                            seconds < 10 ? "0" + seconds : seconds;
                    }, 1000);
                }
            },
            immediate: true,
        },
        timerCount3: {
            handler(value) {
                if (value > 0) {
                    setTimeout(() => {
                        this.timerCount3--;
                        const seconds = Math.floor(
                            (this.timerCount3 % this._minutes) / this._seconds
                        );

                        const minutes = Math.floor(
                            (this.timerCount3 % this._hours) / this._minutes
                        );

                        this.displayMinutes3 =
                            minutes < 10 ? "0" + minutes : minutes;
                        this.displaySeconds3 =
                            seconds < 10 ? "0" + seconds : seconds;
                    }, 1000);
                }
            },
            immediate: true,
        },
        timerCount4: {
            handler(value) {
                if (value > 0) {
                    setTimeout(() => {
                        this.timerCount4--;
                        const seconds = Math.floor(
                            (this.timerCount4 % this._minutes) / this._seconds
                        );

                        const minutes = Math.floor(
                            (this.timerCount4 % this._hours) / this._minutes
                        );

                        this.displayMinutes4 =
                            minutes < 10 ? "0" + minutes : minutes;
                        this.displaySeconds4 =
                            seconds < 10 ? "0" + seconds : seconds;
                        if (
                            this.timerCount1 <= 0 &&
                            this.timerCount2 <= 0 &&
                            this.timerCount3 <= 0 &&
                            this.timerCount4 <= 0
                        ) {
                            this.timerCount1 = 120;
                            this.timerCount2 = 240;
                            this.timerCount3 = 360;
                            this.timerCount4 = 480;
                        }
                    }, 1000);
                }
            },
            immediate: true,
        },
    },
};
</script>

<style scoped lang="scss">
$text-color: brown;
$table-text-color: darken(lightblue, 30%);

.container {
    margin: 10px 20px;
}

.table-container {
    display: grid;
    grid-template-columns: 2 1 1 1 1;
    grid-template-rows: 2 2 auto auto auto auto auto auto;
}

.header-trade {
    font-size: 26px;
    color: $text-color;
    margin-bottom: 0.5rem;
}

.table-header {
    grid-column: 1/2;
    grid-row: 1/2;
    color: $table-text-color;
    // display: flex;
    margin-top: 2rem;
    // width: 15rem;
    display: flex;
    justify-content: center;
    align-items: center;
}

.timer-header {
    color: $text-color;
    width: 15rem;
    height: 2rem;
    margin-top: 2rem;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: lighten($color: $text-color, $amount: 50%);
    border-radius: 100px;
}

.timer-1 {
    grid-column: 2/3;
    grid-row: 1/2;
}

.timer-2 {
    grid-column: 3/4;
    grid-row: 1/2;
}

.timer-3 {
    grid-column: 4/5;
    grid-row: 1/2;
}

.timer-4 {
    grid-column: 5/6;
    grid-row: 1/2;
}

.parametres {
    grid-column: 1/2;
    grid-row: 2/3;
    color: $table-text-color;
    text-transform: uppercase;
    margin-top: 3rem;
    // width: 15rem;
    display: flex;
    justify-content: center;
    // align-items: center;
}

@mixin users {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 15rem;
    color: $table-text-color;
    text-transform: uppercase;
}

.user-1 {
    grid-column: 2/3;
    grid-row: 2/3;
    @include users;
}

.user-2 {
    grid-column: 3/4;
    grid-row: 2/3;
    @include users;
}

.user-3 {
    grid-column: 4/5;
    grid-row: 2/3;
    @include users;
}

.user-4 {
    grid-column: 5/6;
    grid-row: 2/3;
    @include users;
}

.msg-for-traders {
    display: inline-block;
    margin-top: 0.5rem;
    margin-left: 1rem;
    color: $text-color;
    background-color: lighten($text-color, 50%);
    border-radius: 0.5rem;
    padding: 0.3vw;
}

hr {
    background-color: rgb(178, 178, 178);
}

@mixin tableM {
    margin-top: 1rem;
    display: flex;
    justify-content: left;
    align-items: center;
    color: #555;
}

.left-table1 {
    grid-column: 1/2;
    grid-row: 4/5;
    @include tableM();
}
.left-table2 {
    grid-column: 1/2;
    grid-row: 5/6;
    @include tableM();
}
.left-table3 {
    grid-column: 1/2;
    grid-row: 6/7;
    @include tableM();
}
.left-table4 {
    grid-column: 1/2;
    grid-row: 7/8;
    @include tableM();
}
.left-table5 {
    grid-column: 1/2;
    grid-row: 8/9;
    @include tableM();
}
.left-table6 {
    grid-column: 1/2;
    grid-row: 9/10;
    @include tableM();
}

.red {
    color: darken($color: red, $amount: 10%);
    font-weight: 600;
}

.blue {
    color: darken($color: blue, $amount: 20%);
    font-weight: 600;
}
.green {
    color: darken($color: green, $amount: 10%);
    font-weight: 600;
}

@mixin otherTableInfo {
    display: flex;
    justify-content: center;
    align-items: center;
    color: #555;
}

.kompleks1 {
    grid-column: 2/3;
    grid-row: 4/5;
    @include otherTableInfo;
}
.srok1 {
    grid-column: 2/3;
    grid-row: 5/6;
    @include otherTableInfo;
}
.garant1 {
    grid-column: 2/3;
    grid-row: 6/7;
    @include otherTableInfo;
}
.uslovia1 {
    grid-column: 2/3;
    grid-row: 7/8;
    @include otherTableInfo;
}
.stoimost1 {
    grid-column: 2/3;
    grid-row: 8/9;
    display: block;
    justify-self: center;
}

.kompleks2 {
    grid-column: 3/4;
    grid-row: 4/5;
    @include otherTableInfo;
}
.srok2 {
    grid-column: 3/4;
    grid-row: 5/6;
    @include otherTableInfo;
}
.garant2 {
    grid-column: 3/4;
    grid-row: 6/7;
    @include otherTableInfo;
}
.uslovia2 {
    grid-column: 3/4;
    grid-row: 7/8;
    @include otherTableInfo;
}
.stoimost2 {
    grid-column: 3/4;
    grid-row: 8/9;
    display: block;
    justify-self: center;
}

.kompleks3 {
    grid-column: 4/5;
    grid-row: 4/5;
    @include otherTableInfo;
}
.srok3 {
    grid-column: 4/5;
    grid-row: 5/6;
    @include otherTableInfo;
}
.garant3 {
    grid-column: 4/5;
    grid-row: 6/7;
    @include otherTableInfo;
}
.uslovia3 {
    grid-column: 4/5;
    grid-row: 7/8;
    @include otherTableInfo;
}
.stoimost3 {
    grid-column: 4/5;
    grid-row: 8/9;
    display: block;
    justify-self: center;
}

.kompleks4 {
    grid-column: 5/6;
    grid-row: 4/5;
    @include otherTableInfo;
}
.srok4 {
    grid-column: 5/6;
    grid-row: 5/6;
    @include otherTableInfo;
}
.garant4 {
    grid-column: 5/6;
    grid-row: 6/7;
    @include otherTableInfo;
}
.uslovia4 {
    grid-column: 5/6;
    grid-row: 7/8;
    @include otherTableInfo;
}
.stoimost4 {
    grid-column: 5/6;
    grid-row: 8/9;
    display: block;
    justify-self: center;
}
</style>
