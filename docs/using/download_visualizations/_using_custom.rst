.. code-block:: python

  from highcharts_gantt.chart import Chart
  from highcharts_gantt.options.series.gantt import GanttSeries
  from highcharts_gantt.headless_export import ExportServer

  custom_server = ExportServer(url = 'https://www.mydomain.dev/some_pathname_goes_here')

  my_chart = Chart(container = 'target_div',
                   options = {
                       'series': [
                           GanttSeries(data = [ ... ])
                       ]
                   },
                   variable_name = 'myChart',
                   is_gantt_chart = True)

  # Download a PNG version of the chart in memory within your Python code.
  my_png_image = my_chart.download_chart(format = 'png',
                                         server_instance = custom_server)

  # Download a PNG version of the chart and save it the file "/images/my-chart-file.png"
  my_png_image = my_chart.download_chart(
      format = 'png',
      filename = '/images/my-chart-file.png',
      server_instance = custom_server
  )

.. tip::

  **Best practice!**

  If you are using a custom :term:`export server`, it is strongly recommended that you
  supply its configuration (e.g. the URL) via environment variables. For more information,
  please see
  :class:`headless_export.ExportServer <highcharts_gantt.headless_export.ExportServer>`.

.. collapse:: Method Signature

  .. seealso::

    * :meth:`Chart.download_chart() <highcharts_gantt.chart.Chart.download_chart>`
    * :class:`headless_export.ExportServer <highcharts_gantt.headless_export.ExportServer>`

  .. method:: .download_chart(self, filename = None, format = 'png', server_instance = None, scale = 1, width = None, auth_user = None, auth_password = None, timeout = 0.5, global_options = None, **kwargs)
    :noindex:

    Export a downloaded form of the chart using a Highcharts :term:`Export Server`.

    :param filename: The name of the file where the exported chart should (optionally)
      be persisted. Defaults to :obj:`None <python:None>`.
    :type filename: Path-like or :obj:`None <python:None>`

    :param server_instance: Provide an already-configured :class:`ExportServer`
      instance to use to programmatically produce the exported chart. Defaults to
      :obj:`None <python:None>`, which causes **Highcharts for Python** to instantiate
      a new :class:`ExportServer` instance with all applicable defaults.
    :type server_instance: :class:`ExportServer` or :obj:`None <python:None>`

    :param format: The format in which the exported chart should be returned. Defaults to
      ``'png'``.

      Accepts:

        * ``'png'``
        * ``'jpeg'``
        * ``'pdf'``
        * ``'svg'``

    :type format: :class:`str <python:str>`

    :param scale: The scale factor by which the exported chart image should be scaled. Defaults
      to ``1``.

      .. tip::

        Use this setting to improve resolution when exporting PNG or JPEG images. For
        example, setting ``scale = 2`` on a chart whose width is 600px will produce
        an image file with a width of 1200px.

      .. warning::

        If ``width`` is explicitly set, this setting will be *overridden*.

    :type scale: numeric

    :param width: The width that the exported chart should have. Defaults to
      :obj:`None <python:None>`.

      .. warning::

        If explicitly set, this setting will override ``scale``.

    :type width: numeric or :obj:`None <python:None>`

    :param auth_user: The username to use to authenticate against the
      Export Server, using :term:`basic authentication`. Defaults to
      :obj:`None <python:None>`.
    :type auth_user: :class:`str <python:str>` or :obj:`None <python:None>`

    :param auth_password: The password to use to authenticate against the Export
      Server (using :term:`basic authentication`). Defaults to
      :obj:`None <python:None>`.
    :type auth_password: :class:`str <python:str>` or :obj:`None <python:None>`

    :param timeout: The number of seconds to wait before issuing a timeout error.
      The timeout check is passed if bytes have been received on the socket in less
      than the ``timeout`` value. Defaults to ``0.5``.
    :type timeout: numeric or :obj:`None <python:None>`

    :param global_options: The global options which will be passed to the (JavaScript)
      ``Highcharts.setOptions()`` method, and which will be applied to the exported
      chart. Defaults to :obj:`None <python:None>`.

    :type global_options: :class:`HighchartsStockOptions <highcharts_gantt.options.HighchartsStockOptions>`,
      :class:`HighchartsOptions <highcharts_gantt.options.HighchartsOptions>` or
      :obj:`None <python:None>`

    .. note::

      All other keyword arguments are as per the :class:`ExportServer` constructor.

    :returns: The exported chart image, either as a :class:`bytes <python:bytes>`
      binary object or as a base-64 encoded string (depending on the ``use_base64``
      keyword argument).
    :rtype: :class:`bytes <python:bytes>` or :class:`str <python:str>`
