<template lang="html">
    <div class="v-input">
        <div :class="inputClasses">

            <div v-if="$slots.leftAddon" class="input-left-addon">
                <slot name="leftAddon"></slot>
            </div>

            <div :class="fieldClasses" @click="$refs.input.focus()">

                <i v-if="icon" class="input-icon" :class="icon"></i>

                <textarea
                v-if="type == 'textarea'"
                ref="input"
                :value="value"
                :placeholder="placeholderText"
                @input="updateValue($event.target.value);autoresizeTextarea()"
                @focus="isFocus = true"
                @blur="isFocus = false"
                class="input"></textarea>

                <input
                v-else
                ref="input"
                :type="type"
                :value="value"
                :placeholder="placeholderText"
                @input="updateValue($event.target.value)"
                @focus="isFocus = true"
                @blur="isFocus = false"
                class="input">

                <label v-if="label" class="floating-label">{{ label }}</label>

            </div>

            <div v-if="$slots.rightAddon" class="input-right-addon">
                <slot name="rightAddon"></slot>
            </div>
        </div>

        <div v-if="feedback && feedback.text" class="input-help">{{ feedback.text }}</div>
    </div>
</template>

<script>
export default {
    props: {
        /**
         * HTML input type attribute.
         */
        type: {
            type: String,
            default: 'text'
        },

        /**
         * The label text.
         */
        label: {
            type: String
        },

        /**
         * Input placeholder attribute.
         */
        placeholder: {
            type: String
        },

        /**
         * Class of the input icon.
         */
        icon: {
            type: String
        },

        /**
         * Object to render a validation message
         * and applied a theme to the input accordingly.
         */
        feedback: {
            type: Object
        },

        /**
         * Used to bind the value with v-model
         */
        value: {
            type: String
        },

        /**
         * Define if the textarea should be automatically resize.
         */
        autoresize: {
            type: Boolean,
            default: false
        }
    },

    data() {
        return {
            isFocus: false
        }
    },

    computed: {
        /**
         * Classes applied to the input box div.
         * @return {array}
         */
        inputClasses() {
            let classes = ['input-box'];

            if (this.feedback) {
                if (this.feedback.hasOwnProperty('type')) classes.push('has-' + this.feedback.type);
                if (this.feedback.hasOwnProperty('text')) classes.push('has-help');
            }

            if (this.isFocus) classes.push('is-focus');

            return classes;
        },

        /**
         * Classes applied to the field div
         * @return {array}
         */
        fieldClasses() {
            let classes = ['field'];
            if (this.label) classes.push('has-label');
            if (this.icon) classes.push('has-icon');
            return classes;
        },

        /**
         * Set the input placeholder value.
         * @return {string}
         */
        placeholderText() {
            return this.placeholder || `Enter your ${this.label}`;
        }
    },

    methods: {
        /**
        * Emit an input event up to the parent
        */
        updateValue(value) {
            this.$emit('input', value);
        },

        /**
        * Automatically resize the height of the textarea with the content.
        */
        autoresizeTextarea() {
            if (this.autoresize) {
                const textarea = this.$refs.input;
                textarea.style.height = 'auto';
                textarea.style.height = textarea.scrollHeight + 'px';
            }
        },
    }
}
</script>
