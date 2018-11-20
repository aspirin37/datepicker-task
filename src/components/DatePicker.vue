<template>
    <div class="date-picker">
        <label class="date-picker__label">Выберите день недели</label>
        <flat-pickr :config="config"
                    v-model="date"></flat-pickr>
    </div>
</template>
<script>
import flatPickr from 'vue-flatpickr-component';
import 'flatpickr/dist/flatpickr.css';
import { Russian } from 'flatpickr/dist/l10n/ru.js';
export default {
    name: 'DatePicker',
    components: {
        flatPickr
    },
    data() {
        return {
            date: new Date,
            config: {
                locale: Russian,
                altFormat: 'l',
                altInput: true,
                altInputClass: 'date-picker__input',
                onDayCreate: (dObj, dStr, fp, dayElem) => {
                    setTimeout(() => {
                        let cellDate = dayElem.dateObj
                        let selectedDate = new Date(this.date)
                        if (cellDate.getMonth() === selectedDate.getMonth() &&
                            cellDate.getYear() === selectedDate.getYear() &&
                            cellDate.getDay() === selectedDate.getDay() &&
                            cellDate.getDate() > selectedDate.getDate()) {
                            dayElem.classList.add('green-day')
                        }
                    }, 0)
                },
            },
        }
    },
}
</script>
<style lang="scss">
.date-picker {
    margin-top: 100px;
    width: 200px;
    margin: 0 auto;

    &__label {
        display: block;
        text-align: left;
        margin-bottom: 12px;
        cursor: pointer;
    }

    &__input {
        display: block;
        width: 100%;
        padding: .375rem .75rem;
        box-sizing: border-box;
        font-size: 1rem;
        line-height: 1.5;
        color: #495057;
        border: 1px solid #ced4da;
        border-radius: .25rem;
    }
}

.dayContainer .flatpickr-day.today {
    background: red;
    border-color: red;
    color: white;
}

.flatpickr-day.green-day {
    background: #42b883;
    border-color: #42b883;
    color: white;
}
</style>