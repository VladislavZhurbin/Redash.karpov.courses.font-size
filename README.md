# Redash.karpov.courses.font-size
This script will help you change the font size in the editor window to make the coding process more convenient.

// ==UserScript==
// @name         Redash.karpov.courses.font-size
// @namespace    your-namespace
// @version      1.0
// @description  Увеличивает размер шрифта в окне написания SQL запроса в Redash
// @match        https://redash.public.karpov.courses/queries/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';

    // Установите желаемый размер шрифта в пикселях
    var fontSize = '20px';
    var fontSize_autocomplete = '18px';

    // Функция для изменения размера шрифта
    function changeFontSize() {
        var editor = document.getElementsByClassName('ace_editor')[0];
        if (editor) {
            editor.style.fontSize = fontSize;
        }

        var autocomplete = document.getElementsByClassName('ace_autocomplete')[0];
        if (autocomplete) {
            autocomplete.style.fontSize = fontSize_autocomplete;
;
        }
    }

    // Ожидаем загрузку элемента с помощью MutationObserver
    var observer = new MutationObserver(function(mutations) {
        mutations.forEach(function(mutation) {
            if (mutation.addedNodes && mutation.addedNodes.length > 0) {
                changeFontSize();
            }
        });
    });

    // Находим элемент с классом "ace_editor" и начинаем наблюдение за изменениями
    var targetNode = document.body;
    var config = { childList: true, subtree: true };
    observer.observe(targetNode, config);

    // Изменяем размер шрифта сразу после загрузки страницы
    changeFontSize();
})();
