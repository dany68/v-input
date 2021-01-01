<template>
    <div class="v-input">
        <div :class="inputBoxClasses">

            <div v-if="$slots.leftAddon" class="input-left-addon">
                <slot name="leftAddon"></slot>
            </div>

            <div class="field" :class="fieldClasses" @click="$refs.input.focus()">

                <i v-if="icon" class="input-icon" :class="icon"></i>

                <textarea
                v-if="type == 'textarea'"
                ref="input"
                :name="name"
                :value="value"
                :placeholder="placeholderText"
                @input="updateValue($event.target.value);autoresizeTextarea()"
                @focus="isFocus = true"
                @blur="isFocus = false"
                class="input"></textarea>

                <input
                v-else
                ref="input"
                :name="name"
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

        <div v-if="help && !error" class="input-help">{{ help }}</div>
        <div v-if="error" class="input-help">{{ error }}</div>
    </div>
</template>

<script>
export default {
    props: {
        /**
         * The HTML input type attribute.
         */
        type: {
            type: String,
            default: 'text'
        },

        /**
         * The input name attribute.
         */
        name: {
            type: String
        },

        /**
         * If set will add a label.
         * The value will be the label text.
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
         * If set will add an <i> tag and
         * bind this icon prop to the <i> class attribute.
         */
        icon: {
            type: String
        },

        /**
         * Display a help message under the input
         */
        help: {
            type: String
        },

        /**
         * Display an error message
         * and applied a theme to the input accordingly.
         */
        error: {
            type: String
        },

        /**
         * Used to bind the value with v-model.
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
         * Classes to be output on the input box div.
         */
        inputBoxClasses() {
            let classes = ['input-box'];
            if (this.error) classes.push('has-error');
            if (this.isFocus) classes.push('is-focus');
            return classes;
        },

        /**
         * Classes to be output on .field
         */
        fieldClasses() {
            return {
                'has-label': this.label,
                'has-icon': this.icon,
                'is-textarea': this.type == 'textarea'
            }
        },

        /**
         * Set the input placeholder value.
         * @return {string}
         */
        placeholderText() {
            return this.placeholder || `Enter your ${this.label}`;
        }
    },

    methods: {
        /**
        * Emit an input event up to the parent.
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
