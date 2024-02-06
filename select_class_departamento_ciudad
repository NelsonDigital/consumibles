function makeAjaxRequest(url, successCallback) {
        $.ajax({
            url: url,
            dataType: "json",
            type: "GET",
            async: false,
            data: {},
            success: successCallback,
            error: handleAjaxError
        });
    }

    // Función para manejar errores de AJAX
    function handleAjaxError(xhr, exception) {
        var msg = "";
        if (xhr.status === 0) {
            msg = "Not connect.\n Verify Network." + xhr.responseText;
        } else if (xhr.status == 404) {
            msg = "Requested page not found. [404]" + xhr.responseText;
        } else if (xhr.status == 500) {
            msg = "Internal Server Error [500]." + xhr.responseText;
        } else if (exception === "parsererror") {
            msg = "Requested JSON parse failed.";
        } else if (exception === "timeout") {
            msg = "Time out error." + xhr.responseText;
        } else if (exception === "abort") {
            msg = "Ajax request aborted.";
        } else {
            msg = "Error:" + xhr.status + " " + xhr.responseText;
        }
        // Puedes decidir qué hacer con 'msg' en este punto, como mostrar un mensaje de error al usuario.
    }

    // Función para cargar opciones en un elemento select
    function loadOptions(elementId, options) {
        var element = $('.' + elementId);
        element.empty();
        element.append("<option value=''>Seleccione Ciudad*</option>");
        $.each(options, function (index, value) {
            element.prepend("<option value='" + value + "' >" + value + "</option>");
        });
    }

    // Cargar departamentos
    makeAjaxRequest("https://www.datos.gov.co/resource/xdk5-pm3f.json?$select=departamento&$group=departamento&$order=departamento%20DESC", function (data) {
        var departamentos = data.map(function (item) {
            return item.departamento;
        });
        loadOptions("select_departamento", departamentos);
    });

    // Manejar cambio en el departamento
    $('.select_departamento').on('change', function () {
        var valor = this.value;
        makeAjaxRequest("https://www.datos.gov.co/resource/xdk5-pm3f.json?departamento=" + valor + "&$select=municipio&$order=municipio%20ASC", function (data) {
            var municipios = data.map(function (item) {
                return item.municipio;
            });
            loadOptions("select_ciudad", municipios);
        });
    });
